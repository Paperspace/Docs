# Let's Encrypt DNS Providers

Supported list of DNS providers and settings used for Let's Encrypt SSL certificate generation

|  | letsencrypt\_dns\_name | letsencrypt\_dns\_settings |
| :--- | :--- | :--- |
| [ACME DNS](https://github.com/joohoi/acme-dns) | `acme-dns` | `ACME_DNS_API_BASE`, `ACME_DNS_STORAGE_PATH` |
| [Alibaba Cloud](https://www.alibabacloud.com/) | `alidns` | `ALICLOUD_ACCESS_KEY`, `ALICLOUD_SECRET_KEY`, `ALICLOUD_REGION_ID` |
| [Auroradns](https://www.pcextreme.com/aurora/dns) | `auroradns` | `AURORA_USER_ID`, `AURORA_KEY`, `AURORA_ENDPOINT` |
| [Azure](https://azure.microsoft.com/services/dns/) | `azure` | `AZURE_CLIENT_ID`, `AZURE_CLIENT_SECRET`, `AZURE_SUBSCRIPTION_ID`, `AZURE_TENANT_ID`, `AZURE_RESOURCE_GROUP`, `[AZURE_METADATA_ENDPOINT]` |
| [Bindman](https://github.com/labbsr0x/bindman-dns-webhook) | `bindman` | `BINDMAN_MANAGER_ADDRESS` |
| [Blue Cat](https://www.bluecatnetworks.com/) | `bluecat` | `BLUECAT_SERVER_URL`, `BLUECAT_USER_NAME`, `BLUECAT_PASSWORD`, `BLUECAT_CONFIG_NAME`, `BLUECAT_DNS_VIEW` |
| [ClouDNS](https://www.cloudns.net/) | `cloudns` | `CLOUDNS_AUTH_ID`, `CLOUDNS_AUTH_PASSWORD` |
| [Cloudflare](https://www.cloudflare.com/) | `cloudflare` | `CF_API_EMAIL`, `CF_API_KEY` - The `Global API Key` needs to be used, not the `Origin CA Key` |
| [CloudXNS](https://www.cloudxns.net/) | `cloudxns` | `CLOUDXNS_API_KEY`, `CLOUDXNS_SECRET_KEY` |
| [ConoHa](https://www.conoha.jp/) | `conoha` | `CONOHA_TENANT_ID`, `CONOHA_API_USERNAME`, `CONOHA_API_PASSWORD` |
| [DigitalOcean](https://www.digitalocean.com/) | `digitalocean` | `DO_AUTH_TOKEN` |
| [DNSimple](https://dnsimple.com/) | `dnsimple` | `DNSIMPLE_OAUTH_TOKEN`, `DNSIMPLE_BASE_URL` |
| [DNS Made Easy](https://dnsmadeeasy.com/) | `dnsmadeeasy` | `DNSMADEEASY_API_KEY`, `DNSMADEEASY_API_SECRET`, `DNSMADEEASY_SANDBOX` |
| [DNSPod](https://www.dnspod.com/) | `dnspod` | `DNSPOD_API_KEY` |
| [Domain Offensive \(do.de\)](https://www.do.de/) | `dode` | `DODE_TOKEN` |
| [DreamHost](https://www.dreamhost.com/) | `dreamhost` | `DREAMHOST_API_KEY` |
| [Duck DNS](https://www.duckdns.org/) | `duckdns` | `DUCKDNS_TOKEN` |
| [Dyn](https://dyn.com/) | `dyn` | `DYN_CUSTOMER_NAME`, `DYN_USER_NAME`, `DYN_PASSWORD` |
| [EasyDNS](https://easydns.com/) | `easydns` | `EASYDNS_TOKEN`, `EASYDNS_KEY` |
| External Program | `exec` | `EXEC_PATH` |
| [Exoscale](https://www.exoscale.com/) | `exoscale` | `EXOSCALE_API_KEY`, `EXOSCALE_API_SECRET`, `EXOSCALE_ENDPOINT` |
| [Fast DNS](https://www.akamai.com/) | `fastdns` | `AKAMAI_CLIENT_TOKEN`, `AKAMAI_CLIENT_SECRET`, `AKAMAI_ACCESS_TOKEN` |
| [Gandi](https://www.gandi.net/) | `gandi` | `GANDI_API_KEY` |
| [Gandi v5](http://doc.livedns.gandi.net/) | `gandiv5` | `GANDIV5_API_KEY` |
| [Glesys](https://glesys.com/) | `glesys` | `GLESYS_API_USER`, `GLESYS_API_KEY`, `GLESYS_DOMAIN` |
| [GoDaddy](https://godaddy.com/domains) | `godaddy` | `GODADDY_API_KEY`, `GODADDY_API_SECRET` |
| [Google Cloud DNS](https://cloud.google.com/dns/docs/) | `gcloud` | `GCE_PROJECT`, Application Default Credentials \(2\) \(3\), \[`GCE_SERVICE_ACCOUNT_FILE`\] |
| [hosting.de](https://www.hosting.de/) | `hostingde` | `HOSTINGDE_API_KEY`, `HOSTINGDE_ZONE_NAME` |
| HTTP request | `httpreq` | `HTTPREQ_ENDPOINT`, `HTTPREQ_MODE`, `HTTPREQ_USERNAME`, `HTTPREQ_PASSWORD` \(1\) |
| [IIJ](https://www.iij.ad.jp/) | `iij` | `IIJ_API_ACCESS_KEY`, `IIJ_API_SECRET_KEY`, `IIJ_DO_SERVICE_CODE` |
| [INWX](https://www.inwx.de/en) | `inwx` | `INWX_USERNAME`, `INWX_PASSWORD` |
| [Joker.com](https://joker.com/) | `joker` | `JOKER_API_KEY` or `JOKER_USERNAME`, `JOKER_PASSWORD` |
| [Lightsail](https://aws.amazon.com/lightsail/) | `lightsail` | `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `DNS_ZONE` |
| [Linode](https://www.linode.com/) | `linode` | `LINODE_API_KEY` |
| [Linode v4](https://www.linode.com/) | `linodev4` | `LINODE_TOKEN` |
| manual | `manual` | none, but you need to run Traefik interactively, turn on `acmeLogging` to see instructions and press Enter. |
| [MyDNS.jp](https://www.mydns.jp/) | `mydnsjp` | `MYDNSJP_MASTER_ID`, `MYDNSJP_PASSWORD` |
| [Namecheap](https://www.namecheap.com/) | `namecheap` | `NAMECHEAP_API_USER`, `NAMECHEAP_API_KEY` |
| [Namesilo](https://www.namesilo.com/) | `namesilo` | `NAMESILO_API_KEY` |
| [name.com](https://www.name.com/) | `namedotcom` | `NAMECOM_USERNAME`, `NAMECOM_API_TOKEN`, `NAMECOM_SERVER` |
| [Netcup](https://www.netcup.eu/) | `netcup` | `NETCUP_CUSTOMER_NUMBER`, `NETCUP_API_KEY`, `NETCUP_API_PASSWORD` |
| [NIFCloud](https://cloud.nifty.com/service/dns.htm) | `nifcloud` | `NIFCLOUD_ACCESS_KEY_ID`, `NIFCLOUD_SECRET_ACCESS_KEY` |
| [Ns1](https://ns1.com/) | `ns1` | `NS1_API_KEY` |
| [Open Telekom Cloud](https://cloud.telekom.de/) | `otc` | `OTC_DOMAIN_NAME`, `OTC_USER_NAME`, `OTC_PASSWORD`, `OTC_PROJECT_NAME`, `OTC_IDENTITY_ENDPOINT` |
| [OVH](https://www.ovh.com/) | `ovh` | `OVH_ENDPOINT`, `OVH_APPLICATION_KEY`, `OVH_APPLICATION_SECRET`, `OVH_CONSUMER_KEY` |
| [Openstack Designate](https://docs.openstack.org/designate) | `designate` | `OS_AUTH_URL`, `OS_USERNAME`, `OS_PASSWORD`, `OS_TENANT_NAME`, `OS_REGION_NAME` |
| [Oracle Cloud](https://cloud.oracle.com/home) | `oraclecloud` | `OCI_COMPARTMENT_OCID`, `OCI_PRIVKEY_FILE`, `OCI_PRIVKEY_PASS`, `OCI_PUBKEY_FINGERPRINT`, `OCI_REGION`, `OCI_TENANCY_OCID`, `OCI_USER_OCID` |
| [PowerDNS](https://www.powerdns.com/) | `pdns` | `PDNS_API_KEY`, `PDNS_API_URL` |
| [Rackspace](https://www.rackspace.com/cloud/dns) | `rackspace` | `RACKSPACE_USER`, `RACKSPACE_API_KEY` |
| [RFC2136](https://tools.ietf.org/html/rfc2136) | `rfc2136` | `RFC2136_TSIG_KEY`, `RFC2136_TSIG_SECRET`, `RFC2136_TSIG_ALGORITHM`, `RFC2136_NAMESERVER` |
| [Route 53](https://aws.amazon.com/route53/) | `route53` | `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `[AWS_REGION]`, `[AWS_HOSTED_ZONE_ID]` or a configured user/instance IAM profile. |
| [Sakura Cloud](https://cloud.sakura.ad.jp/) | `sakuracloud` | `SAKURACLOUD_ACCESS_TOKEN`, `SAKURACLOUD_ACCESS_TOKEN_SECRET` |
| [Selectel](https://selectel.ru/en/) | `selectel` | `SELECTEL_API_TOKEN` |
| [Stackpath](https://www.stackpath.com/) | `stackpath` | `STACKPATH_CLIENT_ID`, `STACKPATH_CLIENT_SECRET`, `STACKPATH_STACK_ID` |
| [TransIP](https://www.transip.nl/) | `transip` | `TRANSIP_ACCOUNT_NAME`, `TRANSIP_PRIVATE_KEY_PATH` |
| [VegaDNS](https://github.com/shupp/VegaDNS-API) | `vegadns` | `SECRET_VEGADNS_KEY`, `SECRET_VEGADNS_SECRET`, `VEGADNS_URL` |
| [Versio](https://www.versio.nl/domeinnamen) | `versio` | `VERSIO_USERNAME`, `VERSIO_PASSWORD` |
| [Vscale](https://vscale.io/) | `vscale` | `VSCALE_API_TOKEN` |
| [VULTR](https://www.vultr.com/) | `vultr` | `VULTR_API_KEY` |
| [Zone.ee](https://www.zone.ee/) | `zoneee` | `ZONEEE_API_USER`, `ZONEEE_API_KEY` |

