配置流媒体服务器（https://github.com/gwuhaolin/livego）：
1. 他给了两种安装方式，可以用docker, 也可以直接git clone (git clone https://github.com/gwuhaolin/livego.git)。我是直接git clone的
2. cd到livego目录下执行go build或者make build(要有golang)。等待配置完成。
3. make run livego 启动服务器。
4. http://localhost:8090/control/get?room=movie 去这个网址获取一个channel key。这个key 每次重启服务器都会自动变。我没找到固定他的方法暂时。


Webcam端推流：
1. 安装ffmpeg。
2. 查看当前设备中的摄像头和麦克风名称。windows中的命令是：
ffmpeg -list_devices true -f dshow -i dummy
3. 根据查找到的设备名称推流
ffmpeg -f dshow -video_size 800x600 -rtbufsize 1024M -i video="cam_name":audio="MIC_name" -vcodec libx264 -acodec aac -f flv "rtmp://localhost:1935/{appname}/{channelkey}"

rtmp链接举例，这里要用到服务器端查询到的channel key：
"rtmp://192.168.0.53:1935/live/rfBd56ti2SMtYvSgD5xAV0YU99zampta7Z7S575KLkIZ9PYk"


html端拉流：
拉流链接：FLV:http://127.0.0.1:7001/{appname}/movie.flv
这里可以直接用我改好的VirtualFranka_manipulator_0.html替换之前templates中的同名文件。
较之前的html一共有三处改动：
1. head标签下添加了19-20行。
2. 136-140行添加了视频拉流。
3. 542-559添加了js代码。可以把它放在static-assets1-Mycobot280_operation_0.js里面。不改也行。
