---
title: Csharp实现TCP通讯协议
date: 2022-03-05 21:55:26
categories: 开发日记
---

# 概述
Socket的Send方法，并非大家想象中的从一个端口发送消息到另一个端口，它仅仅是拷贝数据到基础系统的发送缓冲区，然后由基础系统将发送缓冲区的数据到连接的另一端口。值得一说的是，这里的拷贝数据与异步发送消息的拷贝是不一样的，同步发送的拷贝，是直接拷贝数据到基础系统缓冲区，拷贝完成后返回，在拷贝的过程中，执行线程会IO等待, 此种拷贝与Socket自带的Buffer空间无关，但异步发送消息的拷贝，是将Socket自带的Buffer空间内的所有数据，拷贝到基础系统发送缓冲区，并立即返回，执行线程无需IO等待，所以异步发送在发送前必须执行SetBuffer方法，拷贝完成后，会触发你自定义回调函数ProcessSend，在ProcessSend方法中，调用SetBuffer方法，重新初始化Buffer空间。

# 客户端代码

``` csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.IO;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Text;
using System.Threading;
using System.Windows.Forms;
using System.Windows;
using System.Collections;

namespace TCPIP
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        Socket socketSend;

        /// <summary>
        /// 向服务器发送消息
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void Form1_Load_1(object sender, EventArgs e)
        {
            Control.CheckForIllegalCrossThreadCalls = false;
        }
        private void button2_Click_1(object sender, EventArgs e)
        {
            //MessageBox.Show(Environment.CurrentDirectory.ToString());
            send(textBox3.Text.Trim());
        }

        private void button1_Click(object sender, EventArgs e)
        {
            try
            {
                //创建客户端Socket，获得远程ip和端口号
                socketSend = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
                IPAddress ip = IPAddress.Parse("127.0.0.1");
                IPEndPoint point = new IPEndPoint(ip, Convert.ToInt32(textBox1.Text));
                socketSend.Connect(point);
                ShowNotice("连接成功!");
                //开启新的线程，不停的接收服务器发来的消息
                Thread c_thread = new Thread(Received);
                c_thread.IsBackground = true;
                c_thread.Start();
            }
            catch (Exception)
            {
                ShowNotice("IP或者端口号错误...");
            }
        }
        void ShowMsg(string str)
        {
            richTextBox1.AppendText(str + "\r\n");
        }
        void ShowNotice(string str)
        {
            textBox4.AppendText(str + "\r\n");
        }
        void send(string msg)
        {
            try
            {
                byte[] buffer = new byte[1024 * 1024 * 3];
                buffer = Encoding.UTF8.GetBytes(msg);
                socketSend.Send(buffer);
            }
            catch { }
        }
        /// <summary>
        /// 接收服务端返回的消息
        /// </summary>
        void Received()
        {
            while (true)
            {
                try
                {
                    byte[] buffer = new byte[1024 * 1024 * 3];
                    //实际接收到的有效字节数
                    int len = socketSend.Receive(buffer);
                    if (len == 0)
                    {
                        break;
                    }
                    string str = Encoding.UTF8.GetString(buffer, 0, len);
                    ShowMsg(socketSend.RemoteEndPoint + ":" + str);
                }
                catch { }
            }
        }
        private void button3_Click(object sender, EventArgs e)
        {
            try
            {
                int a = Convert.ToInt16(textBox2.Text);
                if (a == -1)
                {
                    MessageBox.Show(a.ToString());
                }
            }
            catch { }
        }
    }
}

```

# 服务端代码

``` cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.IO;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Text;
using System.Threading;
using System.Windows.Forms;

namespace TCPIPserve
{
    public partial class Form1 : Form
    {
        
        public TcpListener myListener;
        public TcpClient newClient;
        public BinaryReader br;
        public BinaryWriter bw;
        public int i;
        public Form1()
        {
            InitializeComponent();
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            Control.CheckForIllegalCrossThreadCalls = false;
        }
        /// <summary>
        /// 等待客户端的连接 并且创建与之通信的Socket
        /// </summary>
        Socket socketSend;
        Socket socketWatch;
        void Listen(object o)
        {
            try
            {
                //Socket socketWatch = o as Socket;
                //while (true)
                //{
                socketSend = socketWatch.Accept();//等待接收客户端连接
                ShowMsg(socketSend.RemoteEndPoint.ToString() + ":" + "连接成功!");
                //开启一个新线程，执行接收消息方法
                Thread r_thread = new Thread(Received);
                r_thread.IsBackground = true;
                r_thread.Start();
                //}
            }
            catch { }
        }
        /// <summary>
        /// 服务器端不停的接收客户端发来的消息
        /// </summary>
        /// <param name="o"></param>
        void Received(object o)
        {
            try
            {
                //Socket socketSend = o as Socket;
                while (true)
                {
                    //客户端连接服务器成功后，服务器接收客户端发送的消息
                    byte[] buffer = new byte[1024 * 1024 * 3];
                    //实际接收到的有效字节数
                    int len = socketSend.Receive(buffer);
                    if (len == 0)
                    {
                        break;
                    }
                    string str = Encoding.UTF8.GetString(buffer, 0, len);
                    ShowMsg(socketSend.RemoteEndPoint + ":" + str);
                    if (str == "1")
                    {
                        i = i + 1;
                        textBox1.Text = i.ToString();
                        button3.PerformClick();
                        if (i > 10)
                        {
                            i = 0;
                        }
                    }
                }
            }
            catch { }
        }
        /// <summary>
        /// 服务器向客户端发送消息
        /// </summary>
        /// <param name="str"></param>
        void Send(string str)
        {
            byte[] buffer = Encoding.UTF8.GetBytes(str);
            socketSend.Send(buffer);
        }


        void ShowMsg(string msg)
        {
            richTextBox1.AppendText(msg + "\r\n");
        }
        void ShowNotice(string str)
        {
            textBox3.AppendText(str + "\r\n");
        }
        private void button2_Click_1(object sender, EventArgs e)
        {
            Send(richTextBox2.Text.Trim());
        }
        private void button1_Click_1(object sender, EventArgs e)
        {
            try
            {
                //点击开始监听时 在服务端创建一个负责监听IP和端口号的Socket
                socketWatch = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
                socketSend = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
                IPAddress ip = IPAddress.Parse("127.0.0.1");//任意ip地址都可以
                //创建对象端口
                IPEndPoint point = new IPEndPoint(ip, Convert.ToInt32(textBox2.Text));
                socketWatch.Bind(point);//绑定端口号
                ShowNotice("监听成功!");
                socketWatch.Listen(10);//设置监听

                int point2 = Convert.ToInt32(textBox2.Text);
                TcpListener myListener = new TcpListener(IPAddress.Any, point2);//绑定端口IP信息

                myListener.Start();//开始监听

                TcpClient newClient = myListener.AcceptTcpClient();//接受请求

                newClient.Client.IOControl(IOControlCode.KeepAliveValues, KeepAlive(1, 30000, 10000), null);//设置Keep-Alive参数

                //创建监听线程
                Thread thread = new Thread(Listen);
                thread.IsBackground = true;
                thread.Start();
            }
            catch { }
        }
        
        private byte[] KeepAlive(int onOff, int keepAliveTime, int keepAliveInterval)
        {
            byte[] buffer = new byte[12];
            BitConverter.GetBytes(onOff).CopyTo(buffer, 0);
            BitConverter.GetBytes(keepAliveTime).CopyTo(buffer, 4);
            BitConverter.GetBytes(keepAliveInterval).CopyTo(buffer, 8);
            return buffer;
        }
    }

}

```