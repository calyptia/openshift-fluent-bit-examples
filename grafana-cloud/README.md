# Send logs and metrics to Grafana Cloud from Openshift

Make sure to either export the relevant credentials first or add them to a `.env` file:
```
$ cat .env
export GRAFANA_CLOUD_PROM_USERNAME=XXX
export GRAFANA_CLOUD_LOKI_USERNAME=XXX
export GRAFANA_CLOUD_APIKEY=XXX
export GRAFANA_CLOUD_PROM_URL=prometheus-XXX.grafana.net
export GRAFANA_CLOUD_LOKI_URL=logs-XXX.grafana.net
```

Then we can just use the scripts here:
1. `crc start`
2. [`deploy-helm.sh`](./deploy-helm.sh)

```
$ kubectl logs --namespace fluent-bit-logging $(kubectl get pods --namespace fluent-bit-logging -l "app.kubernetes.io/name=fluent-bit,app.kubernetes.io/instance=fluent-bit" -o jsonpath="{.items[0].metadata.name}")
Fluent Bit v1.8.12
* Copyright (C) 2019-2021 The Fluent Bit Authors
* Copyright (C) 2015-2018 Treasure Data
* Fluent Bit is a CNCF sub-project under the umbrella of Fluentd
* https://fluentbit.io

[2022/03/02 16:35:49] [ info] [engine] started (pid=1)
[2022/03/02 16:35:49] [ info] [storage] version=1.1.5, initializing...
[2022/03/02 16:35:49] [ info] [storage] in-memory
[2022/03/02 16:35:49] [ info] [storage] normal synchronization mode, checksum disabled, max_chunks_up=128
[2022/03/02 16:35:49] [ info] [cmetrics] version=0.2.2
[2022/03/02 16:35:49] [ info] [input:node_exporter_metrics:node_exporter_metrics.0] path.procfs = /proc
[2022/03/02 16:35:49] [ info] [input:node_exporter_metrics:node_exporter_metrics.0] path.sysfs  = /sys
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] multiline core started
[2022/03/02 16:35:49] [ info] [filter:kubernetes:kubernetes.0] https=1 host=kubernetes.default.svc port=443
[2022/03/02 16:35:49] [ info] [filter:kubernetes:kubernetes.0] local POD info OK
[2022/03/02 16:35:49] [ info] [filter:kubernetes:kubernetes.0] testing connectivity with API server...
[2022/03/02 16:35:49] [ info] [filter:kubernetes:kubernetes.0] connectivity OK
[2022/03/02 16:35:49] [ info] [output:loki:loki.1] configured, hostname=logs-prod-eu-west-0.grafana.net:443
[2022/03/02 16:35:49] [ info] [http_server] listen iface=0.0.0.0 tcp_port=2020
[2022/03/02 16:35:49] [ info] [sp] stream processor started
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=61174172 watch_fd=1 name=/var/log/containers/apiserver-56bdf9c9c4-75csf_openshift-apiserver_fix-audit-permissions-4a35747c47d3b9bfbae009d83aff9e20768a22932b276f3f538dbd2efdfccc1c.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=7761005 watch_fd=2 name=/var/log/containers/apiserver-56bdf9c9c4-75csf_openshift-apiserver_openshift-apiserver-bb5f5c4251e5a8cfb80062af652b749c61692621fb9a643e2647b0bed9d7b21a.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=59205312 watch_fd=3 name=/var/log/containers/apiserver-56bdf9c9c4-75csf_openshift-apiserver_openshift-apiserver-check-endpoints-220292fa4f1074cdd50acabe0d9d6f9019596b59dd17161a4b74af4625fda087.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=25289830 watch_fd=4 name=/var/log/containers/apiserver-5c86d888df-8slst_openshift-oauth-apiserver_fix-audit-permissions-934fc5a402c78235a7f33bbea77d2f5de5aa8852cc816fa2c27a9119a0985f85.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=67206159 watch_fd=5 name=/var/log/containers/apiserver-5c86d888df-8slst_openshift-oauth-apiserver_oauth-apiserver-10e50c4f9875fad23e162606b7d4543db73a6a3666a54c12b87b3456d7a4590c.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=54543947 watch_fd=6 name=/var/log/containers/authentication-operator-78cf46778-wpdpt_openshift-authentication-operator_authentication-operator-9db89fdcf0af70f28810a7949126705175824391dffad32e26d3d93e96777a64.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=79821039 watch_fd=7 name=/var/log/containers/catalog-operator-554d4d678d-zrbg8_openshift-operator-lifecycle-manager_catalog-operator-de6c97a8247275f779a7b79ccebae27a69cbc2157bca12f84b8200acf910dd71.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=23118203 watch_fd=8 name=/var/log/containers/certified-operators-7699k_openshift-marketplace_registry-server-9a102534fbf7468e420ab678dc608614d711af0ffe9dd8dacd2074704af779ce.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=42102035 watch_fd=9 name=/var/log/containers/cluster-image-registry-operator-7456697c64-lngr6_openshift-image-registry_cluster-image-registry-operator-409fdf30b31ce0a076d486820e52254cb4442f3b870118e552ecbb78eee7f260.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=56789968 watch_fd=10 name=/var/log/containers/cluster-node-tuning-operator-7654fbbdd6-4dtxl_openshift-cluster-node-tuning-operator_cluster-node-tuning-operator-ba161045bd202b2ff6d53bbabd919c1b18237ef2a54acd480e7edcfe5744265f.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=77908736 watch_fd=11 name=/var/log/containers/cluster-samples-operator-85b98cfdb4-bmf4p_openshift-cluster-samples-operator_cluster-samples-operator-e9de6304ee9ac695723480265597036c114b89dbe3f56702f06f8b6ae9c4e3b6.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=69828885 watch_fd=12 name=/var/log/containers/cluster-samples-operator-85b98cfdb4-bmf4p_openshift-cluster-samples-operator_cluster-samples-operator-watch-d53b5280ae53237524d758a46289db3079402fe9c4abb2c03efe3ad373b5f340.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=33567494 watch_fd=13 name=/var/log/containers/cluster-version-operator-556f59b64-6hm4f_openshift-cluster-version_cluster-version-operator-397c586cc8fa2e7358a7e5d2521f61fb8306ace802ab2a2d3d3ed9cb61991b00.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=5861508 watch_fd=14 name=/var/log/containers/collect-profiles-27437280--1-2llvt_openshift-operator-lifecycle-manager_collect-profiles-7ecfc4427fec42f63ba26a02e8cece77ba7d1f09436bab2f38743e9add764bc5.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=76199810 watch_fd=15 name=/var/log/containers/collect-profiles-27437295--1-hc74m_openshift-operator-lifecycle-manager_collect-profiles-0cf9be59525069e65955066c8efbd52c3b1e5d1986930f10a224457af21a156f.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=13036914 watch_fd=16 name=/var/log/containers/collect-profiles-27437310--1-wkjr4_openshift-operator-lifecycle-manager_collect-profiles-9af1e8808a5702143b33d086539e7948465182e8529d153a679764a72b7234a8.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=44068157 watch_fd=17 name=/var/log/containers/community-operators-mpk2p_openshift-marketplace_registry-server-2e8a5f37085c2062b524c3f04e4bc5843ad0b359f49d149b30e4f01517971d2c.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=65020008 watch_fd=18 name=/var/log/containers/console-5dfb64bd44-nbcgk_openshift-console_console-47f5290a569e6d207cb15756c831a667bdfb0b4bc2890fe3d606d836b96f9a82.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=65375209 watch_fd=19 name=/var/log/containers/console-5dfb64bd44-nbcgk_openshift-console_console-699faa5acb4ac63f02de3d4d325551f8e15da6a47fba32f943d5d787aa754023.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=48556947 watch_fd=20 name=/var/log/containers/console-operator-578d89cbd9-rgj2p_openshift-console-operator_console-operator-de278109893b2765089ec1a1f725a37249fd617252dc4033905e2cface3fa7a8.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=39897425 watch_fd=21 name=/var/log/containers/controller-manager-pjzfh_openshift-controller-manager_controller-manager-e09423cf6611e906bfe99d672763a3c733d9a6d18d92061fdb091df07f2cd0ea.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=9170784 watch_fd=22 name=/var/log/containers/dns-default-5d62k_openshift-dns_dns-6ec9ed38fe38c398c14185b93dd2fdacacd3d1ac13fe682d6ec5cd92dd550b3e.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=12856347 watch_fd=23 name=/var/log/containers/dns-default-5d62k_openshift-dns_kube-rbac-proxy-c92d82e290f27018da041cb4bcbbbd26f17063e67bfa23deae867ec0f56060fc.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=12854146 watch_fd=24 name=/var/log/containers/dns-operator-fdb4c646-x22d4_openshift-dns-operator_dns-operator-b11f21ebc09d0d61e913c939911d0a549ddebd042b77b4ade2575a8815001338.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=9169615 watch_fd=25 name=/var/log/containers/dns-operator-fdb4c646-x22d4_openshift-dns-operator_kube-rbac-proxy-cbda3e2e3bd07991d5e6a7084f3c3f36e034068405c662ed62fcc302b9b27416.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=77908775 watch_fd=26 name=/var/log/containers/downloads-567f47b8f9-49mxk_openshift-console_download-server-6cae8e5c90ab7169297393672d744ea6a52bfbb6da52fcb188d165f96ea7ad83.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=244609 watch_fd=27 name=/var/log/containers/etcd-crc-8rwmc-master-0_openshift-etcd_etcd-1f6bee69ea762f73564e7fdeec115f7a801f3b632a6eb82d52b7eb45fa9d99d4.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=8941442 watch_fd=28 name=/var/log/containers/etcd-crc-8rwmc-master-0_openshift-etcd_etcd-ensure-env-vars-51814c6621013164f2a5d75b1b4461b81237ba9ec6a784ea3d441e4d9e7615fa.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=21028122 watch_fd=29 name=/var/log/containers/etcd-crc-8rwmc-master-0_openshift-etcd_etcd-health-monitor-367a4c30f8235fd81006d8164b513ea12f27399ec7844c17e48747783f7d4bb0.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=65183398 watch_fd=30 name=/var/log/containers/etcd-crc-8rwmc-master-0_openshift-etcd_etcd-metrics-d6bee6e5fa9f7d236e39e8bca75fec978c6ca72dee3a82b0c62ba6ee475af532.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=18882120 watch_fd=31 name=/var/log/containers/etcd-crc-8rwmc-master-0_openshift-etcd_etcd-resources-copy-74adc9ae52f5276ab042b8cc6268e9074b48485bd78e08c70dd4d10ca549d23d.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=48556933 watch_fd=32 name=/var/log/containers/etcd-crc-8rwmc-master-0_openshift-etcd_etcdctl-2b0c402eff26c6930a5722fe0e7c3fadbd9166b3a80f1fe269d4748d6b68d7f8.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=69828872 watch_fd=33 name=/var/log/containers/etcd-crc-8rwmc-master-0_openshift-etcd_setup-ca96ede0701798e8f30d871100140473a1e560b990e6b11d63839032521671c8.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=8391693 watch_fd=34 name=/var/log/containers/etcd-operator-fcd4f986-zjqgq_openshift-etcd-operator_etcd-operator-3d5789e885d1e27744ae767366832dd3f5304bc0b757e63a7c3f84417e25f2d1.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=59205324 watch_fd=35 name=/var/log/containers/image-registry-688d4b9f7f-nw4wr_openshift-image-registry_registry-9318a356ea28a3894704b7519fe3cec5f2c4c0f3bcc1942b3508046232db6a93.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=33753552 watch_fd=36 name=/var/log/containers/ingress-canary-jfbb8_openshift-ingress-canary_serve-healthcheck-canary-309eb09ab779a878ffc073ce2a254fa5126ba9d38fd8861bcf0892aa7d28f0af.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=67205844 watch_fd=37 name=/var/log/containers/ingress-operator-7d56fd784c-7zlb8_openshift-ingress-operator_ingress-operator-316d653e7f17cbdf1ab82b101354a34909631bf6e950f02ee113c7b4d9970524.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=67172317 watch_fd=38 name=/var/log/containers/ingress-operator-7d56fd784c-7zlb8_openshift-ingress-operator_ingress-operator-de8b4c5243482d0c2fd3cc5a9b04f5bae3a27b5208113caedf8ae10edab6bd19.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=56790008 watch_fd=39 name=/var/log/containers/ingress-operator-7d56fd784c-7zlb8_openshift-ingress-operator_kube-rbac-proxy-4e5406b57b62fd1ad3c4723047d049cd50fc386fb8b12ab516b1ad51b83e3b9d.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=44068143 watch_fd=40 name=/var/log/containers/installer-8-crc-8rwmc-master-0_openshift-kube-apiserver_installer-d125b2a8be4ac6694fe6dabef3cac3dcd761d949783ef640a4a9c13a37bb438d.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=59205318 watch_fd=41 name=/var/log/containers/kube-apiserver-crc-8rwmc-master-0_openshift-kube-apiserver_kube-apiserver-9b9d5519b4c93f0354acd13ca41d146d13dbbc9c7ade46fbb8b4bb658aa95819.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=48835441 watch_fd=42 name=/var/log/containers/kube-apiserver-crc-8rwmc-master-0_openshift-kube-apiserver_kube-apiserver-cert-regeneration-controller-804746c07269525c4ee7e8e242c1e137a524923990aa5254d3f42f2bbaa46a83.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=18886905 watch_fd=43 name=/var/log/containers/kube-apiserver-crc-8rwmc-master-0_openshift-kube-apiserver_kube-apiserver-cert-syncer-cf859b422e5460aaeb07eb12c99e5c773c14b2be30dae34f942c756dbcb35514.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=14956272 watch_fd=44 name=/var/log/containers/kube-apiserver-crc-8rwmc-master-0_openshift-kube-apiserver_kube-apiserver-check-endpoints-df3d599b0d4a66c0003a6781a7306b17c10d3e690d3ba3f9b195412aa8ad206c.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=73491701 watch_fd=45 name=/var/log/containers/kube-apiserver-crc-8rwmc-master-0_openshift-kube-apiserver_kube-apiserver-insecure-readyz-dc865d9aaf476bf91599a04cc9c75172754093cd4d0acf5b33a485e691337b08.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=16836842 watch_fd=46 name=/var/log/containers/kube-apiserver-crc-8rwmc-master-0_openshift-kube-apiserver_setup-02c834aba7fd04add204b656dd606a42f470f9066aeaccfbbca5ca655aa418ed.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=48557273 watch_fd=47 name=/var/log/containers/kube-apiserver-operator-5864676c5-bzs4s_openshift-kube-apiserver-operator_kube-apiserver-operator-368e8ca3350aaf93c7d968ae5e86df47d0722df2ba354528f1fb4a4b03601a02.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=12856343 watch_fd=48 name=/var/log/containers/kube-controller-manager-crc-8rwmc-master-0_openshift-kube-controller-manager_cluster-policy-controller-b9bb45bfbabd5f38a60d93d513247366ed3a297488d7538ad6ad5855b3f8c9c4.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=12856342 watch_fd=49 name=/var/log/containers/kube-controller-manager-crc-8rwmc-master-0_openshift-kube-controller-manager_cluster-policy-controller-dca4ef3a7ebc87fd68d7b50ef12f5281930caf882f62eddb0fd89848536789bb.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=59191373 watch_fd=50 name=/var/log/containers/kube-controller-manager-crc-8rwmc-master-0_openshift-kube-controller-manager_kube-controller-manager-71119829802a73a871f912a9c04e3914a3738696c31500b60d49e3144d0ff3fe.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=39893073 watch_fd=51 name=/var/log/containers/kube-controller-manager-crc-8rwmc-master-0_openshift-kube-controller-manager_kube-controller-manager-cert-syncer-54e15c4b777a6b5b79214c9fd54ed715a2e6a4a1a92289800678ca91f08ff28c.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=67188288 watch_fd=52 name=/var/log/containers/kube-controller-manager-crc-8rwmc-master-0_openshift-kube-controller-manager_kube-controller-manager-recovery-controller-9f63592e818a17a6f9ce9914de274bd83c194fdcaec729ebb17e03a2995b8c08.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=65019855 watch_fd=53 name=/var/log/containers/kube-controller-manager-operator-756dffb698-t5jr6_openshift-kube-controller-manager-operator_kube-controller-manager-operator-559a9efede78720db710f3eb916e1783ee239b1fec95eadf732621bd9fd578f4.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=73490586 watch_fd=54 name=/var/log/containers/machine-api-controllers-7649bd8ffc-nct5q_openshift-machine-api_kube-rbac-proxy-machine-mtrc-73d1bc1bcd37a4780f672ca9db598bb75cbe1a687af7a140e629d75e1fcd190c.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=33753562 watch_fd=55 name=/var/log/containers/machine-api-controllers-7649bd8ffc-nct5q_openshift-machine-api_kube-rbac-proxy-machineset-mtrc-c9bbee0ad58677b17d98513b53f1f2c4f64b834ba4420bc7aed1fe23a1a3dfbb.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=44065732 watch_fd=56 name=/var/log/containers/machine-api-controllers-7649bd8ffc-nct5q_openshift-machine-api_kube-rbac-proxy-mhc-mtrc-a557e77f3fa04fc4daea416c425bddc970e61bd40d9421ed17f1210221084dc4.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=25289844 watch_fd=57 name=/var/log/containers/machine-api-controllers-7649bd8ffc-nct5q_openshift-machine-api_machine-controller-510ff0633131eff3d86c7c12660a4c7f0dd6ef8d22bca75c45b97b93ec8df0a1.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=25285545 watch_fd=58 name=/var/log/containers/machine-api-controllers-7649bd8ffc-nct5q_openshift-machine-api_machine-controller-f26eea65347aff119f632f3a371ca5d336ad583649fc28342fe09c208948950e.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=30056782 watch_fd=59 name=/var/log/containers/machine-api-controllers-7649bd8ffc-nct5q_openshift-machine-api_machine-healthcheck-controller-4158dd9171274ddbd65841cf0869f80343d7cdfd40862dde7e8c8f3b19b217c1.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=244503 watch_fd=60 name=/var/log/containers/machine-api-controllers-7649bd8ffc-nct5q_openshift-machine-api_machineset-controller-6d0cbedaefae2264590fef7f35e4f976209e29c90ff7d2771a8a3bf5681e8c10.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=65182856 watch_fd=61 name=/var/log/containers/machine-api-controllers-7649bd8ffc-nct5q_openshift-machine-api_nodelink-controller-969b70020144898eae86e76d818c33f2712d6e7375d10c5e445788d10010b149.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=249035 watch_fd=62 name=/var/log/containers/machine-api-operator-7f456b748f-gg4lz_openshift-machine-api_kube-rbac-proxy-bdc5beed73d2806b5f1373e4a7804fb40b3cf4349e279bfe86dfbefd6ffdf0ee.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=59190278 watch_fd=63 name=/var/log/containers/machine-api-operator-7f456b748f-gg4lz_openshift-machine-api_machine-api-operator-2f5a86780c150917e343ce53a12e511291955a6cbaf703845800b26e122103b7.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=27311811 watch_fd=64 name=/var/log/containers/machine-approver-74559b5df9-6ng9c_openshift-cluster-machine-approver_kube-rbac-proxy-d5bc1c513f60dee05999ddfa6c15ac22ddbf3c65810cf04724dbba8cee3e7175.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=50866829 watch_fd=65 name=/var/log/containers/machine-approver-74559b5df9-6ng9c_openshift-cluster-machine-approver_machine-approver-controller-11123cedb569a4d258273d2cb9824bbf64aa4ef8c1a294d22d01129bf9eb6566.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=50866865 watch_fd=66 name=/var/log/containers/machine-approver-74559b5df9-6ng9c_openshift-cluster-machine-approver_machine-approver-controller-b79941f3762786873e5137e0505271c43b099c75db236095d98b0fd95128da29.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=19361805 watch_fd=67 name=/var/log/containers/machine-config-controller-7594bcbcc5-wkn7k_openshift-machine-config-operator_machine-config-controller-ba6948fc09ca6ae110ccb9edff65dabbe1800237a3c96e8cb8c8965f477b4fd3.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=30051555 watch_fd=68 name=/var/log/containers/machine-config-daemon-pq9lk_openshift-machine-config-operator_machine-config-daemon-89b6c0fe7861fa405abdd333ef187ac5133d346aaddf56b9d985003f08f26604.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=12804173 watch_fd=69 name=/var/log/containers/machine-config-daemon-pq9lk_openshift-machine-config-operator_oauth-proxy-d0e5aaa53cd02f40fc6d40cce2203eb2957f8971bdfa8b763f966ea93210f4cb.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=73414232 watch_fd=70 name=/var/log/containers/machine-config-operator-b8556468-9hrqz_openshift-machine-config-operator_machine-config-operator-488292a746f7d676e493bd31dcf4c29e0c582d33dd68fd01394da1953df6ed85.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=27311812 watch_fd=71 name=/var/log/containers/machine-config-server-cs79d_openshift-machine-config-operator_machine-config-server-4d1933fcafab3ad94d9eecd0cb2810e2b42814defaa8ddd28aa9da05f18e2577.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=54545811 watch_fd=72 name=/var/log/containers/marketplace-operator-58bcd9b996-8j8m7_openshift-marketplace_marketplace-operator-e13f73af18d7e810dcef1f619f662ddef9a255c6f4a0cccd6e81a83403f7c4d4.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=60854164 watch_fd=73 name=/var/log/containers/multus-8qd49_openshift-multus_kube-multus-4362dc662890814275c697c171340357f86289e1754092116c4a239c20fffdac.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=44040321 watch_fd=74 name=/var/log/containers/multus-additional-cni-plugins-gl5xj_openshift-multus_cni-plugins-1d798bcd5aa12e717547b77ffde4bb34cecb5c715c10f0c14672557390840946.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=46612739 watch_fd=75 name=/var/log/containers/multus-additional-cni-plugins-gl5xj_openshift-multus_egress-router-binary-copy-987a45ff11c5a1482ad7c70983ee834d8b51cf007f93ba11d8b9896c7dabe782.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=20317 watch_fd=76 name=/var/log/containers/multus-additional-cni-plugins-gl5xj_openshift-multus_kube-multus-additional-cni-plugins-8f40d3f834e577e94b229760c314a0aa3af3547c0ccb624724128550eb537e71.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=37753861 watch_fd=77 name=/var/log/containers/multus-additional-cni-plugins-gl5xj_openshift-multus_routeoverride-cni-b0b7c0a93336a6577c89225fcf8aed18efefde8d16f559de783a2500ad6fb349.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=27324585 watch_fd=78 name=/var/log/containers/multus-additional-cni-plugins-gl5xj_openshift-multus_whereabouts-cni-74bbb3eb3bb146a8f6e3fa8a6a3342bad49cac7ee877a110ade4d7fdf1f81063.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=54543957 watch_fd=79 name=/var/log/containers/multus-additional-cni-plugins-gl5xj_openshift-multus_whereabouts-cni-bincopy-aa5002b578ece29b7ffb91d691e31fac1ab790f3c1537110cea1523df5a55476.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=48557275 watch_fd=80 name=/var/log/containers/multus-admission-controller-nbm9d_openshift-multus_kube-rbac-proxy-5f413b8b460627739c521214524916c87e11cd8c95d765008744a35aa3f774f6.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=60855445 watch_fd=81 name=/var/log/containers/multus-admission-controller-nbm9d_openshift-multus_multus-admission-controller-2309d8d21860f38680f6f6f9c269c494e360515440f5fd477f73db037138c2d3.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=30056768 watch_fd=82 name=/var/log/containers/network-check-source-79778c7b-s2thk_openshift-network-diagnostics_check-endpoints-4969c90d58041cf5435d96c0455888441cb91460c309d0a4ceb2297182eddaaa.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=27270631 watch_fd=83 name=/var/log/containers/network-check-target-xz4pq_openshift-network-diagnostics_network-check-target-container-b6240db889163f7db88ce3345be7bdb1f69af14c74043db030b610bc8b9f62bb.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=23118953 watch_fd=84 name=/var/log/containers/network-metrics-daemon-wrzbf_openshift-multus_kube-rbac-proxy-7a0246682451ce6b74197095a6bea189407d83eef1869398bedca6aca425467a.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=33753547 watch_fd=85 name=/var/log/containers/network-metrics-daemon-wrzbf_openshift-multus_network-metrics-daemon-4acf91c8514b51fa89ae2e1fdd42947a612d490d9117598296012013300d837e.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=41961733 watch_fd=86 name=/var/log/containers/network-operator-79cb7858bd-xj62d_openshift-network-operator_network-operator-4f647f3164789dec411e37178307a230d0749cac48e942ae18931b2bad4b420c.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=44066882 watch_fd=87 name=/var/log/containers/node-ca-l7gqr_openshift-image-registry_node-ca-5567a0b7cc5b6cb1ca32887071fb8921585cc407e7c6b4080ce592e86fc93144.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=48556937 watch_fd=88 name=/var/log/containers/node-resolver-bvz6g_openshift-dns_dns-node-resolver-e3346feea0615bc365ee12b0c4a9011e91c11d72425ee20f2527dc33bb5ba9c5.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=37873285 watch_fd=89 name=/var/log/containers/oauth-openshift-7f759bf54-h5dxr_openshift-authentication_oauth-openshift-ce11454996b6e0f47af9c444d28bf1fe68608b8a7c2ef55f1e91cf2b729a24ce.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=59190295 watch_fd=90 name=/var/log/containers/olm-operator-5dbb8c7959-pcmj8_openshift-operator-lifecycle-manager_olm-operator-c70b35af66f3710544257ac0c5b549e981839e2d8400c51ba6975d6a29a7c4f4.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=73414220 watch_fd=91 name=/var/log/containers/openshift-apiserver-operator-595488d966-tgfgs_openshift-apiserver-operator_openshift-apiserver-operator-2f8a2bb3b2e7fa066ace7465e5ada9980a471fd5a9b0588a9500ddf14d6a5009.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=71546135 watch_fd=92 name=/var/log/containers/openshift-config-operator-5fc9bd587c-2jtb8_openshift-config-operator_openshift-config-operator-001dbc6c32c925eb24b25f647b74b85ecdff229bec4641465661c27c7672a1ce.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=73414213 watch_fd=93 name=/var/log/containers/openshift-controller-manager-operator-6d8465d654-tlgjm_openshift-controller-manager-operator_openshift-controller-manager-operator-c0c42c212e73e8a28abedbb349b45fc4a6e8e5b94d5e29cbe7eba9626877d6e8.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=53507331 watch_fd=94 name=/var/log/containers/openshift-kube-scheduler-crc-8rwmc-master-0_openshift-kube-scheduler_kube-scheduler-b52ed04b6e88a2653e7408d1b5e757b9f1189586e594ad5408560c5adf6ad530.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=25286727 watch_fd=95 name=/var/log/containers/openshift-kube-scheduler-crc-8rwmc-master-0_openshift-kube-scheduler_kube-scheduler-cert-syncer-8eb5efd70675048e80640f60bf45022e38069ac6e02526dc2ad60464e660d43b.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=53507332 watch_fd=96 name=/var/log/containers/openshift-kube-scheduler-crc-8rwmc-master-0_openshift-kube-scheduler_kube-scheduler-recovery-controller-aa223c54bef65cd83ceebca6c7b4dfb4aba45f5f2139fc5099b5d837be2c7b4e.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=31764488 watch_fd=97 name=/var/log/containers/openshift-kube-scheduler-crc-8rwmc-master-0_openshift-kube-scheduler_wait-for-host-port-577bd3a00babe5883c41184b871f47d8395131530cd623ba03505bb710ff7f31.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=23118144 watch_fd=98 name=/var/log/containers/openshift-kube-scheduler-operator-588bf4dbf7-29v94_openshift-kube-scheduler-operator_kube-scheduler-operator-container-d3e324badf55e1103c18aedb12eea5d02063a8882d943c4ac43459401f23b3eb.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=25286735 watch_fd=99 name=/var/log/containers/package-server-manager-6cc555547d-d4hgm_openshift-operator-lifecycle-manager_package-server-manager-10bb924c5b4d17c3344eaddb0b02e8949d4c91f9f783072bfb36401ae23eaddb.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=71546127 watch_fd=100 name=/var/log/containers/packageserver-76c948d469-xsd7f_openshift-operator-lifecycle-manager_packageserver-78f9ba2e5ed861bc0e8d93ad6d88ffa5501e4779b272dc2f09dd754ef7c23439.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=42064985 watch_fd=101 name=/var/log/containers/redhat-marketplace-vhc4v_openshift-marketplace_registry-server-e5a4162fb0f59c8b444f35d06ed3bd0b7fb03cc5145107a07894569718ceb849.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=52480133 watch_fd=102 name=/var/log/containers/redhat-operators-w54rv_openshift-marketplace_registry-server-e8b6f703a9986940c5df84528beff4095abb0542c65068686c8cb6801989be14.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=77906014 watch_fd=103 name=/var/log/containers/revision-pruner-7-crc-8rwmc-master-0_openshift-kube-apiserver_pruner-5baa68d13dc069f632e1cb99b0561fef01578d5ad577ba5ddccc7d3f8fe92740.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=14955506 watch_fd=104 name=/var/log/containers/revision-pruner-7-crc-8rwmc-master-0_openshift-kube-controller-manager_pruner-430b1c61d9702eb9ff6c56ef55d8d48afaa7efb2605afedc40ab37b3769f4ae4.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=69860306 watch_fd=105 name=/var/log/containers/revision-pruner-8-crc-8rwmc-master-0_openshift-kube-apiserver_pruner-d7d5a8ecb3436e4b373b51ead8a8037ab5f6546c2ed78f35ea34478da86778c6.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=37937532 watch_fd=106 name=/var/log/containers/revision-pruner-8-crc-8rwmc-master-0_openshift-kube-scheduler_pruner-07e2260227dc77f0a8a5ea1137e6e0cc17139b8105cd08e8cd9dbd8d553d01cc.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=27407885 watch_fd=107 name=/var/log/containers/router-default-7bd9b9c9ff-tnjk9_openshift-ingress_router-1c0f2ee87b6b08a18153b8d816e0a209a16c3c17ca01d1e005a970ecc8274561.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=27344768 watch_fd=108 name=/var/log/containers/router-default-7bd9b9c9ff-tnjk9_openshift-ingress_router-24ce9a065e18c80cca1931955035e6afe6ad6682e4afd4de4a0365579ad41002.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=77601244 watch_fd=109 name=/var/log/containers/sdn-controller-96fcg_openshift-sdn_sdn-controller-397fdc52c7768cc615cf29549c86d16de3c95e9c773f4b58799e1335df64f1cc.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=50764762 watch_fd=110 name=/var/log/containers/sdn-lstzh_openshift-sdn_kube-rbac-proxy-b86ba2a36701cd2e53c9239ae4ce381f3b76ef814c46842f3c922c5aee4cea98.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=62963883 watch_fd=111 name=/var/log/containers/sdn-lstzh_openshift-sdn_sdn-2a8f353bb0c2722daad000e0f3a2d37f29d12ec1e66678783e8cd0a57cfb151b.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=59190300 watch_fd=112 name=/var/log/containers/service-ca-69d4cd64c7-pk2qx_openshift-service-ca_service-ca-controller-ca7186acedaaa04d52b7c01bd858cc9bd16983294ecd7c720786610adf507234.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=21094157 watch_fd=113 name=/var/log/containers/service-ca-operator-668487d9b9-sgnx2_openshift-service-ca-operator_service-ca-operator-09bf205324329df9b3f49efd668011c605d3b8f4e35e54283e0a949bb3a3af13.log
[2022/03/02 16:35:49] [ info] [input:tail:tail.1] inotify_fs_add(): inode=23077317 watch_fd=114 name=/var/log/containers/tuned-wkqhh_openshift-cluster-node-tuning-operator_tuned-20f3dbd3185e8c000885c09ea74f2c99e9ac9bf061a7b4fef212567e5e47f76e.log
[2022/03/02 16:35:52] [ info] [output:prometheus_remote_write:prometheus_remote_write.0] prometheus-prod-01-eu-west-0.grafana.net:443, HTTP status=200
[2022/03/02 16:35:53] [ info] [output:prometheus_remote_write:prometheus_remote_write.0] prometheus-prod-01-eu-west-0.grafana.net:443, HTTP status=200
[2022/03/02 16:35:56] [ info] [output:prometheus_remote_write:prometheus_remote_write.0] prometheus-prod-01-eu-west-0.grafana.net:443, HTTP status=200
[2022/03/02 16:35:57] [ info] [output:prometheus_remote_write:prometheus_remote_write.0] prometheus-prod-01-eu-west-0.grafana.net:443, HTTP status=200
[2022/03/02 16:35:59] [ info] [output:prometheus_remote_write:prometheus_remote_write.0] prometheus-prod-01-eu-west-0.grafana.net:443, HTTP status=200
[2022/03/02 16:36:01] [ info] [output:prometheus_remote_write:prometheus_remote_write.0] prometheus-prod-01-eu-west-0.grafana.net:443, HTTP status=200
[2022/03/02 16:36:04] [ info] [output:prometheus_remote_write:prometheus_remote_write.0] prometheus-prod-01-eu-west-0.grafana.net:443, HTTP status=200
[2022/03/02 16:36:05] [ info] [output:prometheus_remote_write:prometheus_remote_write.0] prometheus-prod-01-eu-west-0.grafana.net:443, HTTP status=200
```