# Nuclei

Nuclei是一款注重于可配置性、可扩展性和易用性的基于模板的快速漏洞扫描器。

```
用法：
  nuclei [命令]

命令：
目标：
   -u, -target string[]                  指定扫描的目标URL/主机（多个目标则指定多个-u参数）
   -l, -list string                      指定包含要扫描的目标URL/主机列表的文件路径（一行一个）
   -resume string                        使用指定的resume.cfg文件恢复扫描（将禁用请求聚类）
   -sa, -scan-all-ips                    扫描由目标解析出来的所有IP（针对域名对应多个IP的情况）
   -iv, -ip-version string[]             要扫描的主机名的IP版本（4,6）-（默认为4）

模板：
   -nt, -new-templates                    仅运行最新发布的nuclei模板
   -ntv, -new-templates-version string[]  仅运行特定版本中添加的新模板
   -as, -automatic-scan                   基于Wappalyzer技术的标签映射自动扫描
   -t, -templates string[]                指定要运行的模板或者模板目录（以逗号分隔或目录形式）
   -turl, -template-url string[]          指定要运行的模板URL或模板目录URL（以逗号分隔或目录形式）
   -w, -workflows string[]                指定要运行的工作流或工作流目录（以逗号分隔或目录形式）
   -wurl, -workflow-url string[]          指定要运行的工作流URL或工作流目录URL（以逗号分隔或目录形式）
   -validate                              使用nuclei验证模板有效性
   -nss, -no-strict-syntax                禁用对模板的严格检查
   -td, -template-display                 显示模板内容
   -tl                                    列出所有可用的模板
   -sign                                  使用NUCLEI_SIGNATURE_PRIVATE_KEY环境变量中的私钥对模板进行签名
   -code                                  启用加载基于协议的代码模板

过滤：
   -a, -author string[]                  执行指定作者的模板（逗号分隔，文件）
   -tags string[]                        执行带指定tag的模板（逗号分隔，文件）
   -etags, -exclude-tags string[]        排除带指定tag的模板（逗号分隔，文件）
   -itags, -include-tags string[]        执行带有指定tag的模板，即使是被默认或者配置排除的模板
   -id, -template-id string[]            执行指定id的模板（逗号分隔，文件）
   -eid, -exclude-id string[]            排除指定id的模板（逗号分隔，文件）
   -it, -include-templates string[]      执行指定模板，即使是被默认或配置排除的模板
   -et, -exclude-templates string[]      排除指定模板或者模板目录（逗号分隔，文件）
   -em, -exclude-matchers string[]       排除指定模板matcher
   -s, -severity value[]                 根据严重程度运行模板，可选值有：info,low,medium,high,critical   
   -es, -exclude-severity value[]        根据严重程度排除模板，可选值有：info,low,medium,high,critical
   -pt, -type value[]                    根据类型运行模板，可选值有：dns, file, http, headless, network, workflow, ssl, websocket, whois
   -ept, -exclude-type value[]           根据类型排除模板，可选值有：dns, file, http, headless, network, workflow, ssl, websocket, whois
   -tc, -template-condition string[]     根据表达式运行模板
   

输出：
   -o, -output string                    输出发现的问题到文件
   -sresp, -store-resp                   将nuclei的所有请求和响应输出到目录
   -srd, -store-resp-dir string          将nuclei的所有请求和响应输出到指定目录（默认：output）
   -silent                               只显示结果
   -nc, -no-color                        禁用输出内容着色（ANSI转义码）
   -j, -jsonl                            输出格式为jsonL（ines）
   -irr, -include-rr                     在JSON、JSONL和Markdown中输出请求/响应对（仅结果）[已弃用，使用-omit-raw替代]
   -or, -omit-raw                        在JSON、JSONL和Markdown中不输出请求/响应对
   -ot, -omit-template           省略JSON、JSONL输出中的编码模板
   -nm, -no-meta                         在cli输出中不打印元数据
   -ts, -timestamp                       在cli输出中打印时间戳
   -rdb, -report-db string               本地的nuclei结果数据库（始终使用该数据库保存结果）
   -ms, -matcher-status                  显示匹配失败状态
   -me, -markdown-export string          以markdown格式导出结果
   -se, -sarif-export string             以SARIF格式导出结果
   -je, -json-export string              以JSON格式导出结果
   -jle, -jsonl-export string            以JSONL(ine)格式导出结果


配置：
   -config string                        指定nuclei的配置文件
   -fr, -follow-redirects                为HTTP模板启用重定向
   -fhr, -follow-host-redirects          允许在同一主机上重定向
   -mr, -max-redirects int               HTTP模板最大重定向次数（默认：10）
   -dr, -disable-redirects               为HTTP模板禁用重定向
   -rc, -report-config string            指定nuclei报告模板文件
   -H, -header string[]                  指定在所有http请求中包含的自定义header、cookie，以header:value的格式指定（cli，文件）
   -V, -var value                        以key=value格式自定义变量
   -r, -resolvers string                 指定包含DNS解析服务列表的文件
   -sr, -system-resolvers                当DNS错误时使用系统DNS解析服务
   -dc, -disable-clustering              关闭请求聚类功能
   -passive                              启用被动模式处理本地HTTP响应数据
   -fh2, -force-http2                    强制使用http2连接
   -ev, env-vars                         启用在模板中使用环境变量
   -cc, -client-cert string              用于对扫描的主机进行身份验证的客户端证书文件（PEM 编码）
   -ck, -client-key string               用于对扫描的主机进行身份验证的客户端密钥文件（PEM 编码）
   -ca, -client-ca string                用于对扫描的主机进行身份验证的客户端证书颁发机构文件（PEM 编码）
   -sml, -show-match-line                显示文件模板的匹配值，只适用于提取器
   -ztls                                 使用ztls库，带有自动回退到标准库tls13 [已弃用] 默认情况下启用对ztls的自动回退
   -sni string                           指定tls sni的主机名（默认为输入的域名）
   -lfa, -allow-local-file-access        允许访问本地文件（payload文件）
   -lna, -restrict-local-network-access  阻止对本地/私有网络的连接
   -i, -interface string                 指定用于网络扫描的网卡
   -at, -attack-type string              payload的组合模式（batteringram,pitchfork,clusterbomb）
   -sip, -source-ip string               指定用于网络扫描的源IP
   -rsr, -response-size-read int         最大读取响应大小（默认：10485760字节）
   -rss, -response-size-save int         最大储存响应大小（默认：1048576字节）
   -reset                                删除所有nuclei配置和数据文件（包括nuclei-templates）
   -tlsi, -tls-impersonate               启用实验性的Client Hello（ja3）TLS 随机化功能


交互：
   -inserver, -ineractsh-server string   使用interactsh反连检测平台（默认为oast.pro,oast.live,oast.site,oast.online,oast.fun,oast.me）
   -itoken, -interactsh-token string     指定反连检测平台的身份凭证
   -interactions-cache-size int          指定保存在交互缓存中的请求数（默认：5000）
   -interactions-eviction int            从缓存中删除请求前等待的时间（默认为60秒）
   -interactions-poll-duration int       每个轮询前等待时间（默认为5秒）
   -interactions-cooldown-period int     退出轮询前的等待时间（默认为5秒）
   -ni, -no-interactsh                   禁用反连检测平台，同时排除基于反连检测的模板


模糊测试:
   -ft, -fuzzing-type string             覆盖模板中设置的模糊测试类型（replace、prefix、postfix、infix）
   -fm, -fuzzing-mode string             覆盖模板中设置的模糊测试模式（multiple、single）


UNCOVER引擎:
   -uc, -uncover                         启动uncover引擎
   -uq, -uncover-query string[]          uncover查询语句
   -ue, -uncover-engine string[]         指定uncover查询引擎 （shodan,censys,fofa,shodan-idb,quake,hunter,zoomeye,netlas,criminalip,publicwww,hunterhow） （默认 shodan）
   -uf, -uncover-field string            查询字段 （ip,port,host） （默认 "ip:port"）
   -ul, -uncover-limit int               查询结果数 （默认 100）
   -ur, -uncover-ratelimit int           查询速率，默认每分钟60个请求（默认 60）


限速：
   -rl, -rate-limit int                  每秒最大请求量（默认：150）
   -rlm, -rate-limit-minute int          每分钟最大请求量
   -bs, -bulk-size int                   每个模板最大并行检测数（默认：25）
   -c, -concurrency int                  并行执行的最大模板数量（默认：25）
   -hbs, -headless-bulk-size int         每个模板并行运行的无头主机最大数量（默认：10）
   -headc, -headless-concurrency int     并行指定无头主机最大数量（默认：10）


优化：
   -timeout int                          超时时间（默认为10秒）
   -retries int                          重试次数（默认：1）
   -ldp, -leave-default-ports            指定HTTP/HTTPS默认端口（例如：host:80，host:443）
   -mhe, -max-host-error int             某主机扫描失败次数，跳过该主机（默认：30）
   -te, -track-error string[]            将给定错误添加到最大主机错误监视列表（标准、文件）
   -nmhe, -no-mhe                        disable skipping host from scan based on errors
   -project                              使用项目文件夹避免多次发送同一请求
   -project-path string                  设置特定的项目文件夹
   -spm, -stop-at-first-path             得到一个结果后停止（或许会中断模板和工作流的逻辑）
   -stream                               流模式 - 在不整理输入的情况下详细描述
   -ss, -scan-strategy value             扫描时使用的策略（auto/host-spray/template-spray） （默认 auto）
   -irt, -input-read-timeout duration    输入读取超时时间（默认：3分钟）
   -nh, -no-httpx                        禁用对非URL输入进行httpx探测
   -no-stdin                             禁用标准输入

无界面浏览器：
    -headless                            启用需要无界面浏览器的模板
    -page-timeout int                    在无界面下超时秒数（默认：20）
    -sb, -show-brower                    在无界面浏览器运行模板时，显示浏览器
    -ho, -headless-options string[]      使用附加选项启动无界面浏览器
    -sc, -system-chrome                  不使用Nuclei自带的浏览器，使用本地浏览器
    -lha, -list-headless-action          列出可用的无界面操作

调试：
    -debug                               显示所有请求和响应
    -dreq, -debug-req                    显示所有请求
    -dresp, -debug-resp                  显示所有响应
    -p, -proxy string[]                  使用http/socks5代理（逗号分隔，文件）
    -pi, -proxy-internal                 代理所有请求
    -ldf, -list-dsl-function             列出所有支持的DSL函数签名
    -tlog, -trace-log string             写入跟踪日志到文件
    -elog, -error-log string             写入错误日志到文件
    -version                             显示版本信息
    -hm, -hang-monitor                   启用对nuclei挂起协程的监控
    -v, -verbose                         显示详细信息
    -profile-mem string                  将Nuclei的内存转储成文件
    -vv                                  显示额外的详细信息
    -svd, -show-var-dump                 显示用于调试的变量输出
    -ep, -enable-pprof                   启用pprof调试服务器
    -tv, -templates-version              显示已安装的模板版本
    -hc, -health-check                   运行诊断检查

升级：
    -up, -update                         更新Nuclei到最新版本
    -ut, -update-templates               更新Nuclei模板到最新版
    -ud, -update-template-dir string     指定模板目录
    -duc, -disable-update-check          禁用nuclei程序与模板更新

统计：
    -stats                               显示正在扫描的统计信息
    -sj, -stats-json                     将统计信息以JSONL格式输出到文件
    -si, -stats-inerval int              显示统计信息更新的间隔秒数（默认：5）
    -mp, -metrics-port int               更改metrics服务的端口（默认：9092）

云服务：
   -auth                  配置projectdiscovery云服务（pdcp）API密钥
   -cup, -cloud-upload    将扫描结果上传到pdcp仪表板
   -sid, -scan-id string  将扫描结果上传到指定的扫描ID

例子:
扫描一个单独的URL:
	$ nuclei -target example.com

对URL运行指定的模板:
	$ nuclei -target example.com -t http/cves/ -t ssl

扫描hosts.txt中的多个URL:
	$ nuclei -list hosts.txt

输出结果为JSON格式:
	$ nuclei -target example.com -json-export output.json

使用已排序的Markdown输出（使用环境变量）运行nuclei:
	$ MARKDOWN_EXPORT_SORT_MODE=template nuclei -target example.com -markdown-export nuclei_report/
```