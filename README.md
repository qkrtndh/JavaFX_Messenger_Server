# JavaFX_Messenger_Server

<H1>TCP/IP 소켓통신을 이용한 Java 메신저 프로그램</H1>

<H2>1. TCP/IP</H2>
<p>TCP는 IP주소를 통해 동작하는 프로토콜로 데이터의 전달을 보증하고 보낸 순서대로 받게 한다.</P>
<P>IP는 Internet Protocol규약/규칙에 의해 부여된 주소 IP Address이다.</P>

<H2>2. 포트(Port)</H2>
<P>IP주소가 동사무소 입구라고 한다면 포트는 각 창구 라고 볼 수 있다.</P>
<P>IP주소 만으로는 어떠한 이유로 어디에 접근하는지 알 수 없기 때문에 목적에 따라 포트를 나누어 해당 기능을 필요로 하는 접근을 나눈다.</P>
<P>포트는 0~65535 까지 존재하나 0~1023 까지는 시스템에서 사용하기 때문에 사용자는 1024~65535 사이의 포트를 사용할 수 있다.</P>

<H2>3. 소켓 통신(Socket)</H2>
<P>소켓은 각 포트를 사용하여 통신을 수행하는 도구이다.</P>
<P>각 프로그램에 포트를 할당하는 것 만으로는 통신이 불가능하며, 소켓을 통해 데이터를 주고받는다.</P>
<P>즉 소켓은 각 창구의 직원이라고 생각할 수 있다.</P>

<P>서버측의 소켓은 생성된 후 클라이언트 소켓의 연결요청을 기다리며 대기한다.</P>
<P>클라이언트 소켓은 별도의 대기없이 바로 서버소켓에 연결요청을 한다.</P>
<P>연결요청을 받은 서버소켓은 서버측의 클라이언트소켓을 생성하여 통신을 가능하게 한다.</P>
<P>이후 클라이언트 소켓을 이용해 통신이 이루어진다.</P>

<H2>구현 개요</H2>
<img src = "https://t1.daumcdn.net/cfile/tistory/99FFD1345ED62D7B31"/>

<P>소켓생성시 매개변수로 IP와 포트를 넣어준다면 자동으로 연결을 시도한다.</P>
<P>데이터는 스트림 형태로 주고받게 되며 OutputStream은 데이터를 보낼때 InputStream은 받을 때 사용된다.</P>
<P>1대n의 통신이 가능하게 하기 위해 Thread를 사용한다 클라이언트 측은 보내고 받는 스레드 두개만 존재한다</P>
<P>서버측은 클라이언트 클래스(클라이언트의 어플리케이션이 아닌 서버측이 개별 클래스임) 를 통해 각 클라이언트들이 접근할때 마다 쓰레드를 생성한다.</P>
<P>기본 쓰레드는 생성된쓰레드를 서버클래스의 스레드풀에 등록한다.</P>
<P>서버의 각 쓰레드는 클라이언트가 메세지를 전송하기를 기다리다 메세지가 도착하면 해당 메세지를 모든 클라이언트에 전송한다.</P>