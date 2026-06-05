KCT(Kill Class Tool) 云控指令使用手册
一、判断条件
1.运行
RUN
2.检测到任意U盘
CHECK_U
3.检测到指定名称的U盘
CHECK_U_NAME 名称
4.检测到无名称U盘
CHECK_U_NM
5.检测到指定大小的U盘
CHECK_U_SIZE 大小（KB）
6.检测到特定进程名
CHECK_P_NAME 进程名
7.检测到特定窗口标题
CHECK_W_NAME 窗口标题
二、运行任务
1.调试用
PRINT 打印内容
2.修改U盘名称
SET_U_NAME 原名称 现名称
3.删除指定U盘中的所有课件文件（.ppt .pptx .doc .docx .pdf .rtf .xls .xlsx）
DELETE_U_KJ U盘名
4.破坏指定U盘中的所有课件文件（.ppt .pptx .doc .docx .pdf .rtf .xls .xlsx）
CORRUPT_U_KJ U盘名 文件头破坏总比特数 全文件破坏总比特数
5.删除无名称U盘中的所有课件文件（.ppt .pptx .doc .docx .pdf .rtf .xls .xlsx）
DELETE_U_KJ_NM
6.破坏无名称U盘中的所有课件文件（.ppt .pptx .doc .docx .pdf .rtf .xls .xlsx）
CORRUPT_U_KJ_NM 文件头破坏总比特数 全文件破坏总比特数
7.遍历删除指定U盘里所有文件名包含特定字符的文件
DELETE_U_NF U盘名 python列表格式的需删除的字符串
8.遍历破坏指定U盘里所有文件名包含特定字符的文件
CORRUPT_U_NF U盘名 python列表格式的需破坏的字符串 文件头破坏总比特数 全文件破坏总比特数
9.遍历删除无名称U盘里所有文件名包含特定字符的文件
DELETE_U_NF_NM python列表格式的需删除的字符串
10.遍历破坏无名称U盘里所有文件名包含特定字符的文件
CORRUPT_U_NF_NM python列表格式的需破坏的字符串 文件头破坏总比特数 全文件破坏总比特数
11.杀死指定进程
KILL_P 进程名
12.挂起指定进程
SUSPEND_P 进程名
13.恢复指定进程
RESUME_P 进程名
14.设置标题包含关键词的窗口为可穿透
TM_W python列表格式的需设为穿透的窗口名关键词
15.恢复标题包含关键词的窗口为可穿透
TM_UW python列表格式的需恢复穿透的窗口名关键词
16.设置指定进程的所有窗口可穿透
TM_P_W 进程名
17.恢复指定进程的所有窗口可穿透
TM_P_UW 进程名
18.终止标题包含关键词的窗口背后的进程
KILL_W python列表格式的需关闭的窗口名关键词
19.挂起标题包含关键词的窗口背后的进程
SUSPEND_W python列表格式的需挂起的窗口名关键词
20.恢复标题包含关键词的窗口背后的进程
RESUME_W python列表格式的需恢复的窗口名关键词
21.鼠标点击
MOUSE_CLICK 左键右键中键（left/right/middle） 点击次数（可选） 点击间隔（可选）
22.鼠标移动（绝对）
MOUSE_MOVE x坐标 y坐标 移动时间
23.鼠标移动（相对）
MOUSE_MOVE_R x距离 y距离 移动时间
24.键盘按下
KEYBOARD_KD 按键
25.键盘抬起
KEYBOARD_KU 按键
26.键盘输入（英文）
KEYBOARD_WRITE 内容
21.windows风格弹窗
MSGBOX 标题 内容 弹窗图标（info：提示，warning：警告，error：错误，question：问号）
22.退出
EXIT
23.立即自毁
SELF_DELETE sure_to_delete
24.执行cmd指令
CMD python字符串格式的命令（需自行加引号）
三、语法
签名（下文指令除去首尾空字符）
判断条件1
延时执行时间1>运行任务1
延时执行时间2>运行任务2
判断条件2
延时执行时间3>运行任务3
延时执行时间4>运行任务4

判断条件的具体语法：
判断指令 参数1 参数2
以上方式的判断程序每次启动只会执行一次
~判断指令 参数1 参数2
以上方式的判断每次检测如果满足条件都会执行

判断延时时间的具体语法：
a;b;c;d
其中a是第一次启动的延时，b是循环执行的次数，c是每次循环的等待时间（单位都是秒）
需要随机数时，a，b，c均可以表示为111r222，表示从111到222的随机浮点数。
d是每一次循环变化的变量，格式为AAA=i#BBB=2i#CCC=3i
其中#为分隔符，以AAA=i距离，这个指令会把后续指令中的所有AAA替换为=后面的Python表达式执行的结果（转化为字符串）
完整的举例：
0;15r20;0.001r0.2;I=i#aaa=(i*i)/2+10#aaaaaaa=random.randint(0,i)*"sss"#logo=["info","warning","error","question"][random.randint(0,3)]>MSGBOX TESTMSG,num=I TESTMSG,testnum=aaa,aaaaaaa logo