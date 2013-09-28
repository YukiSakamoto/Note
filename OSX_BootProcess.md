## MacOSXのブートプロセス
(Source: http://www.tuaw.com/2010/10/22/mac-101-whats-happening-when-your-mac-is-starting-up/)

### 電源投入〜ブートチャイムがなるまで
電源をいれるとまず、Macのハードウェアの初期化がおこり、その後でFirmware(BootROM)がロード＆実行される。

- BootROMはMacのマザーボード上のフラッシュメモリーに格納されていて、それだけで小さなOSみたいに動く。
	
- FirmwareはPOST(: Power-On Self Test)と呼ばれるシステムテストで、プロセッサー、システムメモリ、ネットワーク(Wi-Fi, Ethernet)やPeripheral(USB, FireWire, Bluetooth) インターフェースなどのチェックをする。
	
- このテストが通れば、スタートアップチャイムがなって、Firmwareはブートファイル（ブート可能なファイル）をさがしにかかる。
	
- 仮にテストにFailしたらどうなるか。
		
	- ディスプレイは何も表示されないまま、またはエラーコードが表示されるだけ。あとはエラーを示す音がでる？とりあえずAppleのGeneusにASAPで聞くべき。
	
	

### グレーの画面にアップルロゴが表示された状態

- Firmwareはあらかじめ、システムのブートファイルがどこにあるかをしっている。

	- ブートファイルのロケーションはnonvolatile RAM(NVRAM)に保存されている。
	
	- これはシステム環境設定=> 起動ディスク（またはWindowsのブートキャンプ設定パネル）
	
			多分、ブートファイルってのはEFI,　つまりブートローダのことを示しているんだと思う。

- ブートファイルが見つかったら、EFI(Extensible Firmware Interface)がブーロプロセスをスタートさせ、MacOSXまたはBootcampを設定している場合はWindowsのブートにかかる。

	- この時点で、スタートアップの仕方をカスタマイズするコマンドが使える。
		
		- C DVDまたはCDからのブート
		
		- T MacをFireWireでTarget Disk Modeでスタートする。これによって古いMacのハードディスクにアクセスして、データや設定を移すのに役立つ。
		
		- Option Statup Managerを起動し、どのボリュームで起動するかなど選べるようにする。ブートキャンプとかで有用。
		
		- Shift セーフモードで起動。より詳細にスタートアッププロセスを起動し、なおかつ自動で起動されるプロセスを最小限に制限する。
		
		- Command-V VerboseMode（饒舌モード）で起動する。これによって、スタートアッププロセスでUNIXの中で何が起こっているかよくわかる。グレーの画面の代わりに黒い背景のうえにテキストがひたすら表示。
		
		- Command-Option-P-R NVRAMの設置をリセットし、Macを再起動する。PRはParameter RAMから来てる。

### スピニングギアが表示されるところ
MacのFirmwareによってブートプロセスがスタートされた状態。二つのことが起こっている。

- Mac OS Xカーネルのロード、カーネルエクステンション（KEXTs）のロード。これによりカーネルはシステム全体を利用し、スタートアップを続行できる。

- カーネルのロードが成功したら、暗い灰色のスピニングギアアイコンをアップルのロゴの下に見る事ができる。この時、launchedプロセスが起動し他の全てのプロセスをspawnする。

### ブルーの画面がでるところ（この解説はSnow Leopard以前のみたい）
- Windows-baseのものだが、この時点ではまだシステムの初期化プロセスが進行中。

- 明るいブルーの画面が表示されている間はlaunched プロセスがWindow Serverプロセスをフォークしたことをしめす。このWindows ServerプロセスがMac OS Xのユーザーインターフェースを表示する。

- この後で、loginwindow.app（これはバックグラウンドプロセス）が開始する。これはログインウィンドウとかユーザーデスクトップを表示する。


### ほかのリソース

http://osxbook.com/book/bonus/ancient/whatismacosx/arch_boot.html





