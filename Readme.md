# How to log HTTP request header and cookie values to Tomcat access logs

We have modified the following part of server.xml:

    <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
           prefix="localhost_access_log" suffix=".txt"
           pattern="%h %l %u %t &quot;%r&quot; %s %b header1Value: %{HEADER1}i, cookiesValue: '%{Cookie}i'" />


To see it in action run:

    docker run -it --rm -p 8888:8080 -v $(pwd)/server.xml:/usr/local/tomcat/conf/server.xml -v $(pwd)/logs/:/usr/local/tomcat/logs/ tomcat:9.0

Now send a request with a header and some cookies:
    
    curl --header "HEADER1: 56744373z111" --cookie "COOKIE1=766;COOKIE2=444" http://localhost:8888/

And see the logs in logs/localhost_access_log...txt file
