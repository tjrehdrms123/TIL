![](/study/assets/thumbnail_liunx.png)

# 👿 SemrushBot 악성 봇 접근 차단하기

### 사용하는 AWS서버의 호스팅에 521에러가 발생했습니다 그 이유와 문제점에 대해서 알아보겠습니다


**CloudWatch에 대한 로그입니다 Cpu, 서버로 접근하는 Network가 비선형적으로 증가했습니다**
![](/study/assets/content_liunx_bot_graph.png)

**예상해 볼 수 있는 원인에 대해서**

1. 서비스 사용자가 늘어나서 네트워크와 CPU 사용량 증가


2. BF(brute-force) 공격


**프로세스 확인(top)**
서버에 CPU를 잡아먹는 프로세스 확인했습니다
apache2 프로세스가 CPU사용량이 100%로 확인되었습니다 그래서 내부 문제로 확인했습니다
![](/study/assets/content_liunx_bot_blocking.png)

**에러로그 분석**
apache의 access.log 로그 분석 중 compatible; SemrushBot 봇의 접근을 확인했습니다

**로봇의 접근을 막는 config파일 생성**
- /etc/httpd/conf.d/bad_bot.con
```shell
<Directory "/var/www/htdocs/*">  ## 여기는 자신의 서버 상황에 맞게 수정
 
# SetEnvIfNoCase User-Agent ^$ bad_bot
SetEnvIfNoCase User-Agent "^MJ12bot" bad_bot
SetEnvIfNoCase User-Agent "^MJ12bot/v1.4.5" bad_bot
 
 
#악성봇...
SetEnvIfNoCase User-Agent "SemrushBot" bad_bot          #181203
SetEnvIfNoCase User-Agent "SemrushBot-SA" bad_bot       #181203
SetEnvIfNoCase User-Agent "DomainCrawler" bad_bot       #181210
SetEnvIfNoCase User-Agent "MegaIndex.ru" bad_bot        #181215
SetEnvIfNoCase User-Agent "AlphaBot" bad_bot            #181219
 
#기타 귀찮은 것들
SetEnvIfNoCase User-Agent "ltx71" bad_bot
SetEnvIfNoCase User-Agent "CCBot" bad_bot
SetEnvIfNoCase User-Agent "Sogou" bad_bot
SetEnvIfNoCase User-Agent "DotBot" bad_bot
SetEnvIfNoCase User-Agent "PiplBot" bad_bot
SetEnvIfNoCase User-Agent "MJ12bot" bad_bot
SetEnvIfNoCase User-Agent "AhrefsBot" bad_bot
SetEnvIfNoCase User-Agent "MauiBot" bad_bot
SetEnvIfNoCase User-Agent "AhrefsBot" bad_bot
SetEnvIfNoCase User-Agent "ezooms" bad_bot
SetEnvIfNoCase User-Agent "sistrix" bad_bot
SetEnvIfNoCase User-Agent "Yandex" bad_bot
 
 
# Block Bad Bots & Scrapers
SetEnvIfNoCase User-Agent "Aboundex" bad_bot
SetEnvIfNoCase User-Agent "80legs" bad_bot
SetEnvIfNoCase User-Agent "360Spider" bad_bot
SetEnvIfNoCase User-Agent "^Java" bad_bot
SetEnvIfNoCase User-Agent "^Cogentbot" bad_bot
SetEnvIfNoCase User-Agent "^Alexibot" bad_bot
SetEnvIfNoCase User-Agent "^asterias" bad_bot
SetEnvIfNoCase User-Agent "^attach" bad_bot
SetEnvIfNoCase User-Agent "^BackDoorBot" bad_bot
SetEnvIfNoCase User-Agent "^BackWeb" bad_bot
SetEnvIfNoCase User-Agent "Bandit" bad_bot
SetEnvIfNoCase User-Agent "^BatchFTP" bad_bot
SetEnvIfNoCase User-Agent "^Bigfoot" bad_bot
SetEnvIfNoCase User-Agent "^Black.Hole" bad_bot
SetEnvIfNoCase User-Agent "^BlackWidow" bad_bot
SetEnvIfNoCase User-Agent "^BlowFish" bad_bot
SetEnvIfNoCase User-Agent "^BotALot" bad_bot
SetEnvIfNoCase User-Agent "Buddy" bad_bot
SetEnvIfNoCase User-Agent "^BuiltBotTough" bad_bot
SetEnvIfNoCase User-Agent "^Bullseye" bad_bot
SetEnvIfNoCase User-Agent "^BunnySlippers" bad_bot
SetEnvIfNoCase User-Agent "^Cegbfeieh" bad_bot
SetEnvIfNoCase User-Agent "^CheeseBot" bad_bot
SetEnvIfNoCase User-Agent "^CherryPicker" bad_bot
SetEnvIfNoCase User-Agent "^ChinaClaw" bad_bot
SetEnvIfNoCase User-Agent "Collector" bad_bot
SetEnvIfNoCase User-Agent "Copier" bad_bot
SetEnvIfNoCase User-Agent "^CopyRightCheck" bad_bot
SetEnvIfNoCase User-Agent "^cosmos" bad_bot
SetEnvIfNoCase User-Agent "^Crescent" bad_bot
SetEnvIfNoCase User-Agent "^Custo" bad_bot
SetEnvIfNoCase User-Agent "^AIBOT" bad_bot
SetEnvIfNoCase User-Agent "^DISCo" bad_bot
SetEnvIfNoCase User-Agent "^DIIbot" bad_bot
SetEnvIfNoCase User-Agent "^DittoSpyder" bad_bot
SetEnvIfNoCase User-Agent "^Download\ Demon" bad_bot
SetEnvIfNoCase User-Agent "^Download\ Devil" bad_bot
SetEnvIfNoCase User-Agent "^Download\ Wonder" bad_bot
SetEnvIfNoCase User-Agent "^dragonfly" bad_bot
SetEnvIfNoCase User-Agent "^Drip" bad_bot
SetEnvIfNoCase User-Agent "^eCatch" bad_bot
SetEnvIfNoCase User-Agent "^EasyDL" bad_bot
SetEnvIfNoCase User-Agent "^ebingbong" bad_bot
SetEnvIfNoCase User-Agent "^EirGrabber" bad_bot
SetEnvIfNoCase User-Agent "^EmailCollector" bad_bot
SetEnvIfNoCase User-Agent "^EmailSiphon" bad_bot
SetEnvIfNoCase User-Agent "^EmailWolf" bad_bot
SetEnvIfNoCase User-Agent "^EroCrawler" bad_bot
SetEnvIfNoCase User-Agent "^Exabot" bad_bot
SetEnvIfNoCase User-Agent "^Express\ WebPictures" bad_bot
SetEnvIfNoCase User-Agent "Extractor" bad_bot
SetEnvIfNoCase User-Agent "^EyeNetIE" bad_bot
SetEnvIfNoCase User-Agent "^Foobot" bad_bot
SetEnvIfNoCase User-Agent "^flunky" bad_bot
SetEnvIfNoCase User-Agent "^FrontPage" bad_bot
SetEnvIfNoCase User-Agent "^Go-Ahead-Got-It" bad_bot
SetEnvIfNoCase User-Agent "^gotit" bad_bot
SetEnvIfNoCase User-Agent "^GrabNet" bad_bot
SetEnvIfNoCase User-Agent "^Grafula" bad_bot
SetEnvIfNoCase User-Agent "^Harvest" bad_bot
SetEnvIfNoCase User-Agent "^hloader" bad_bot
SetEnvIfNoCase User-Agent "^HMView" bad_bot
SetEnvIfNoCase User-Agent "^HTTrack" bad_bot
SetEnvIfNoCase User-Agent "^humanlinks" bad_bot
SetEnvIfNoCase User-Agent "^IlseBot" bad_bot
SetEnvIfNoCase User-Agent "^Image\ Stripper" bad_bot
SetEnvIfNoCase User-Agent "^Image\ Sucker" bad_bot
SetEnvIfNoCase User-Agent "Indy\ Library" bad_bot
SetEnvIfNoCase User-Agent "^InfoNaviRobot" bad_bot
SetEnvIfNoCase User-Agent "^InfoTekies" bad_bot
SetEnvIfNoCase User-Agent "^Intelliseek" bad_bot
SetEnvIfNoCase User-Agent "^InterGET" bad_bot
SetEnvIfNoCase User-Agent "^Internet\ Ninja" bad_bot
SetEnvIfNoCase User-Agent "^Iria" bad_bot
SetEnvIfNoCase User-Agent "^Jakarta" bad_bot
SetEnvIfNoCase User-Agent "^JennyBot" bad_bot
SetEnvIfNoCase User-Agent "^JetCar" bad_bot
SetEnvIfNoCase User-Agent "^JOC" bad_bot
SetEnvIfNoCase User-Agent "^JustView" bad_bot
SetEnvIfNoCase User-Agent "^Jyxobot" bad_bot
SetEnvIfNoCase User-Agent "^Kenjin.Spider" bad_bot
SetEnvIfNoCase User-Agent "^Keyword.Density" bad_bot
SetEnvIfNoCase User-Agent "^larbin" bad_bot
SetEnvIfNoCase User-Agent "^LexiBot" bad_bot
SetEnvIfNoCase User-Agent "^lftp" bad_bot
SetEnvIfNoCase User-Agent "^libWeb/clsHTTP" bad_bot
SetEnvIfNoCase User-Agent "^likse" bad_bot
SetEnvIfNoCase User-Agent "^LinkextractorPro" bad_bot
SetEnvIfNoCase User-Agent "^LinkScan/8.1a.Unix" bad_bot
SetEnvIfNoCase User-Agent "^LNSpiderguy" bad_bot
SetEnvIfNoCase User-Agent "^LinkWalker" bad_bot
SetEnvIfNoCase User-Agent "^lwp-trivial" bad_bot
SetEnvIfNoCase User-Agent "^LWP::Simple" bad_bot
SetEnvIfNoCase User-Agent "^Magnet" bad_bot
SetEnvIfNoCase User-Agent "^Mag-Net" bad_bot
SetEnvIfNoCase User-Agent "^MarkWatch" bad_bot
SetEnvIfNoCase User-Agent "^Mass\ Downloader" bad_bot
SetEnvIfNoCase User-Agent "^Mata.Hari" bad_bot
SetEnvIfNoCase User-Agent "^Memo" bad_bot
SetEnvIfNoCase User-Agent "^Microsoft.URL" bad_bot
SetEnvIfNoCase User-Agent "^Microsoft\ URL\ Control" bad_bot
SetEnvIfNoCase User-Agent "^MIDown\ tool" bad_bot
SetEnvIfNoCase User-Agent "^MIIxpc" bad_bot
SetEnvIfNoCase User-Agent "^Mirror" bad_bot
SetEnvIfNoCase User-Agent "^Missigua\ Locator" bad_bot
SetEnvIfNoCase User-Agent "^Mister\ PiX" bad_bot
SetEnvIfNoCase User-Agent "^moget" bad_bot
SetEnvIfNoCase User-Agent "^Mozilla/3.Mozilla/2.01" bad_bot
SetEnvIfNoCase User-Agent "^Mozilla.*NEWT" bad_bot
SetEnvIfNoCase User-Agent "^NAMEPROTECT" bad_bot
SetEnvIfNoCase User-Agent "^Navroad" bad_bot
SetEnvIfNoCase User-Agent "^NearSite" bad_bot
SetEnvIfNoCase User-Agent "^NetAnts" bad_bot
SetEnvIfNoCase User-Agent "^Netcraft" bad_bot
SetEnvIfNoCase User-Agent "^NetMechanic" bad_bot
SetEnvIfNoCase User-Agent "^NetSpider" bad_bot
SetEnvIfNoCase User-Agent "^Net\ Vampire" bad_bot
SetEnvIfNoCase User-Agent "^NetZIP" bad_bot
SetEnvIfNoCase User-Agent "^NextGenSearchBot" bad_bot
SetEnvIfNoCase User-Agent "^NG" bad_bot
SetEnvIfNoCase User-Agent "^NICErsPRO" bad_bot
SetEnvIfNoCase User-Agent "^niki-bot" bad_bot
SetEnvIfNoCase User-Agent "^NimbleCrawler" bad_bot
SetEnvIfNoCase User-Agent "^Ninja" bad_bot
SetEnvIfNoCase User-Agent "^NPbot" bad_bot
SetEnvIfNoCase User-Agent "^Octopus" bad_bot
SetEnvIfNoCase User-Agent "^Offline\ Explorer" bad_bot
SetEnvIfNoCase User-Agent "^Offline\ Navigator" bad_bot
SetEnvIfNoCase User-Agent "^Openfind" bad_bot
SetEnvIfNoCase User-Agent "^OutfoxBot" bad_bot
SetEnvIfNoCase User-Agent "^PageGrabber" bad_bot
SetEnvIfNoCase User-Agent "^Papa\ Foto" bad_bot
SetEnvIfNoCase User-Agent "^pavuk" bad_bot
SetEnvIfNoCase User-Agent "^pcBrowser" bad_bot
SetEnvIfNoCase User-Agent "^PHP\ version\ tracker" bad_bot
SetEnvIfNoCase User-Agent "^Pockey" bad_bot
SetEnvIfNoCase User-Agent "^ProPowerBot/2.14" bad_bot
SetEnvIfNoCase User-Agent "^ProWebWalker" bad_bot
SetEnvIfNoCase User-Agent "^psbot" bad_bot
SetEnvIfNoCase User-Agent "^Pump" bad_bot
SetEnvIfNoCase User-Agent "^QueryN.Metasearch" bad_bot
SetEnvIfNoCase User-Agent "^RealDownload" bad_bot
SetEnvIfNoCase User-Agent "Reaper" bad_bot
SetEnvIfNoCase User-Agent "Recorder" bad_bot
SetEnvIfNoCase User-Agent "^ReGet" bad_bot
SetEnvIfNoCase User-Agent "^RepoMonkey" bad_bot
SetEnvIfNoCase User-Agent "^RMA" bad_bot
SetEnvIfNoCase User-Agent "Siphon" bad_bot
SetEnvIfNoCase User-Agent "^SiteSnagger" bad_bot
SetEnvIfNoCase User-Agent "^SlySearch" bad_bot
SetEnvIfNoCase User-Agent "^SmartDownload" bad_bot
SetEnvIfNoCase User-Agent "^Snake" bad_bot
SetEnvIfNoCase User-Agent "^Snapbot" bad_bot
SetEnvIfNoCase User-Agent "^Snoopy" bad_bot
SetEnvIfNoCase User-Agent "^sogou" bad_bot
SetEnvIfNoCase User-Agent "^SpaceBison" bad_bot
SetEnvIfNoCase User-Agent "^SpankBot" bad_bot
SetEnvIfNoCase User-Agent "^spanner" bad_bot
SetEnvIfNoCase User-Agent "^Sqworm" bad_bot
SetEnvIfNoCase User-Agent "Stripper" bad_bot
SetEnvIfNoCase User-Agent "Sucker" bad_bot
SetEnvIfNoCase User-Agent "^SuperBot" bad_bot
SetEnvIfNoCase User-Agent "^SuperHTTP" bad_bot
SetEnvIfNoCase User-Agent "^Surfbot" bad_bot
SetEnvIfNoCase User-Agent "^suzuran" bad_bot
SetEnvIfNoCase User-Agent "^Szukacz/1.4" bad_bot
SetEnvIfNoCase User-Agent "^tAkeOut" bad_bot
SetEnvIfNoCase User-Agent "^Teleport" bad_bot
SetEnvIfNoCase User-Agent "^Telesoft" bad_bot
SetEnvIfNoCase User-Agent "^TurnitinBot/1.5" bad_bot
SetEnvIfNoCase User-Agent "^The.Intraformant" bad_bot
SetEnvIfNoCase User-Agent "^TheNomad" bad_bot
SetEnvIfNoCase User-Agent "^TightTwatBot" bad_bot
SetEnvIfNoCase User-Agent "^Titan" bad_bot
SetEnvIfNoCase User-Agent "^True_Robot" bad_bot
SetEnvIfNoCase User-Agent "^turingos" bad_bot
SetEnvIfNoCase User-Agent "^TurnitinBot" bad_bot
SetEnvIfNoCase User-Agent "^URLy.Warning" bad_bot
SetEnvIfNoCase User-Agent "^Vacuum" bad_bot
SetEnvIfNoCase User-Agent "^VCI" bad_bot
SetEnvIfNoCase User-Agent "^VoidEYE" bad_bot
SetEnvIfNoCase User-Agent "^Web\ Image\ Collector" bad_bot
SetEnvIfNoCase User-Agent "^Web\ Sucker" bad_bot
SetEnvIfNoCase User-Agent "^WebAuto" bad_bot
SetEnvIfNoCase User-Agent "^WebBandit" bad_bot
SetEnvIfNoCase User-Agent "^Webclipping.com" bad_bot
SetEnvIfNoCase User-Agent "^WebCopier" bad_bot
SetEnvIfNoCase User-Agent "^WebEMailExtrac.*" bad_bot
SetEnvIfNoCase User-Agent "^WebEnhancer" bad_bot
SetEnvIfNoCase User-Agent "^WebFetch" bad_bot
SetEnvIfNoCase User-Agent "^WebGo\ IS" bad_bot
SetEnvIfNoCase User-Agent "^Web.Image.Collector" bad_bot
SetEnvIfNoCase User-Agent "^WebLeacher" bad_bot
SetEnvIfNoCase User-Agent "^WebmasterWorldForumBot" bad_bot
SetEnvIfNoCase User-Agent "^WebReaper" bad_bot
SetEnvIfNoCase User-Agent "^WebSauger" bad_bot
SetEnvIfNoCase User-Agent "^Website\ eXtractor" bad_bot
SetEnvIfNoCase User-Agent "^Website\ Quester" bad_bot
SetEnvIfNoCase User-Agent "^Webster" bad_bot
SetEnvIfNoCase User-Agent "^WebStripper" bad_bot
SetEnvIfNoCase User-Agent "^WebWhacker" bad_bot
SetEnvIfNoCase User-Agent "^WebZIP" bad_bot
SetEnvIfNoCase User-Agent "Whacker" bad_bot
SetEnvIfNoCase User-Agent "^Widow" bad_bot
SetEnvIfNoCase User-Agent "^WISENutbot" bad_bot
SetEnvIfNoCase User-Agent "^WWWOFFLE" bad_bot
SetEnvIfNoCase User-Agent "^WWW-Collector-E" bad_bot
SetEnvIfNoCase User-Agent "^Xaldon" bad_bot
SetEnvIfNoCase User-Agent "^Xenu" bad_bot
SetEnvIfNoCase User-Agent "^Zeus" bad_bot
SetEnvIfNoCase User-Agent "ZmEu" bad_bot
SetEnvIfNoCase User-Agent "^Zyborg" bad_bot
 
# Vulnerability Scanners
SetEnvIfNoCase User-Agent "Acunetix" bad_bot
SetEnvIfNoCase User-Agent "FHscan" bad_bot
 
# Aggressive Chinese Search Engine
SetEnvIfNoCase User-Agent "Baiduspider" bad_bot
 
   
     Require all granted
     Require not env bad_bot
```

참고 URL : [https://xetown.com/tips/1130812](https://xetown.com/tips/1130812)