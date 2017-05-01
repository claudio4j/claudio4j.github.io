---
id: 35
title: SJSAS 7 working on Linux (Kernel 2.6.x)
date: 2005-01-25T05:11:19+00:00
author: Claudio Miranda
layout: post
permalink: /2005/01/SJSAS-7-working-on-Linux-Kernel-2-6-x/
categories:
  - Java
---
<big><big><big><span style="font-weight: bold;">Installing (and<br /> hacking) Sun Java System Application Server 7 on Linux</span></big></big></big>

<big style="font-weight: bold;"><big>Preface</big></big>

&nbsp;&nbsp;&nbsp; Sun Java System Application Server 7 is the J2EE 1.3
  
Application Server from Sun Microsystems. The supported Linux operating
  
system is RedHat Enterprise Linux 2.1 and 3.0. Any other Linux
  
operating system is not supported, but that
  
doesn&#8217;t stop anyone to install Sun Java System Application Server 7 on
  
any Linux distribution, but that doesn&#8217;t have any warranty nor
  
endorsement from Sun. I will call Sun Java System Application Server 7
  
of SJSAS7 to make it easy.
  
&nbsp;&nbsp;&nbsp; SJSAS7 can be installed on any Linux distribution,
  
which has Kernel 2.4.x, I did that on Mandrake Linux 9.2. But for a
  
unknown reason, the SJSAS7 Installation process doesn&#8217;t work on Linux
  
Kernel 2.6.x.
  
&nbsp;&nbsp;&nbsp; My system is a Mandrake Linux Official 10.1 and a
  
custom kernel 2.6.10 with patches, so my system is an unsupported one.
  
I was tired to switch to windows, just to run SJSAS 7, and it is
  
supposed to be entirely implemented in Java (but Sun WebServer is not
  
Java), then I just need to try to do a hack and make it work on linux.
  
After 6 hours it is done. 
  
&nbsp;&nbsp;&nbsp; This howto can be found on line at: [http://www.claudius.com.br/blog/claudio/Java/2005/01/25/SJSAS\_7\_working\_on\_Linux\_Kernel\_2\_6\_x.html](http://www.claudius.com.br/blog/claudio/Java/2005/01/25/SJSAS_7_working_on_Linux_Kernel_2_6_x.html)

Written by: [Claudio
  
Miranda](mailto:claudio%28@%29CLAUDIUS.com.br)

<big style="font-weight: bold;"><big>Warranties</big></big>

&nbsp;&nbsp;&nbsp; Sun Microsystems doesn&#8217;t have any involvement
  
related to
  
this document.
  
&nbsp;&nbsp;&nbsp; I don&#8217;t give any warranty about this document, and I
  
am not responsible to software or hardware damage.

<big style="font-weight: bold;"><big>Requirements</big></big>

&#8211; Sun Java System Application Server 7 for linux: sunappserver7.tar.gz
  
&nbsp; I used SJSAS 7 2004Q2 Update 1
  
&nbsp; <a target="_blank"
href="http://www.sun.com/download/index.jsp?cat=Application%20%26%20Integration%20Services&tab=3&subcat=Application%20Servers">http://www.sun.com/download/index.jsp?cat=Application%20%26%20Integration%20Services&tab=3&subcat=Application%20Servers</a>
  
&#8211; An already installed SJSAS 7, preferably on linux
  
&nbsp; I used a sparc installation
  
&nbsp; I will call it SJSAS7-REF, that will serve as reference of
  
configuration for the linux instance
  
&#8211; A running JVM 1.4.2 or greater
  
&nbsp; If you don&#8217;t want to install the SJSAS7 bundled JDK
  
&nbsp; eg: /opt/j2sdk1.4.2_06

<big style="font-weight: bold;"><big>Installation</big></big>

  * Make a backup of some directories of SJSAS7-REF
  * SJSAS7-REF/config
  * SJSAS7-REF/bin 

  * Untar the downloaded SJSAS7, eg:
  
    UNTAR=/home/claudio/sunappserver-7

  * Create the directory to install SJSAS 7, eg:
  
    /opt/sjsas7-2004Q2-up1
  
    I will call it: SJSAS7 

  * cd /opt/sjsas7-2004Q2-up1

  * unzip $UNTAR/packages/*.zip
  * exceptions:
  * If you don&#8217;t want to install a new JDK, don&#8217;t unzip jdk.zip
  * if you don&#8217;t want pointbase, don&#8217;t unzip SUNWasdbo.zip
  * $UNTAR/packages/ant.zip
  * $UNTAR/packages/perl.zip

  * Some files is duplicated across some zip files, you can replace
  
    them safely. 

  * ANT installation
  * mkdir lib/ant
  * cd lib/ant
  * unzip $UNTAR/packages/ant.zip 

  * Perl Installation
  * mkdir lib/perl
  * cd lib/perl
  * unzip $UNTAR/packages/perl.zip 



  * copy $SJSAS7-REF/bin to $SJSAS7/bin
  * copy $SJSAS7-REF/config to $SJSAS7/config
  * mkdir $SJSAS7/domains

<big style="font-weight: bold;"><big>Configuration</big></big>

Some adjustments on configuration files needs to be done for the newly
  
linux installment.

What needs to be adjusted:

  * J2SE SDK location
  * SJSAS 7 home location
  * Native JVM lib (if the SJSAS7-REF is solaris) 

  * cd $SJSAS7/bin 
  * Each script file, at the beginning has the full path of the
  
    asenv.conf file, adjust it to reflect your installment
  
    eg: <span style="font-weight: bold;">.<br /> /opt/sjsas7-2004Q2-up1/config/asenv.conf</span> 

<div style="margin-left: 40px;">
  You can use the following command:</p> 
  
  <p>
    find . | xargs perl -i.bkp -p -e<br /> &#8216;s/\/opt\/sjsas7-ref/\/opt\/sjsas7-2004Q2-up1/g;&#8217;
  </p>
  
  <p>
    Where:
  </p>
  
  <ul>
    <li>
      -i: do a backup of each file
    </li>
    <li>
      -e: runs the specified regular expression
    </li>
    <li>
      -p: reads each line of the file
    </li>
  </ul>
</div>

  * cd ../config
  * Edit asenv.conf, adjust the directory to reflect your
  
    environment
  * SJSAS7 home, eg: /opt/sjsas7-2004Q2-up1
  * JDK_HOME 

  * The $SJSAS7/config/domains.bin file needs to be reflect the
  
    current environment
  * run asadmin list-domains, that will show the domain list, eg:
  
    /sunappserver7/domains/domain1
  
    /sunappserver7/domains/test
  * And the SJSAS7 is located under /opt/sjsas7-2004Q2-up1, the
  
    domains need to be under this directory
  * create the following directories
  
    /sunappserver7/domains/domain1
  
    /sunappserver7/domains/test
  * run asadmin delete-domain domain1 and delete-domain test
  * remove the /sunappserver7 directory
  * create new domain and instance 
  * asadmin create-domain &#8211;path&nbsp;
  
    /ope/sjsas7-2004Q2-up1/domains/ &#8211;adminport 4881 &#8211;adminuser admin
  
    &#8211;adminpassword admin123 domain1

<big style="font-weight: bold;"><big>Final Notes</big></big>

  * Do a search on the SJSAS7 home
  * grep -Hr <SJSAS7-REF> $SJSAS7
  
    eg: grep -Hr SUNWappserver /opt/sjsas7-2004Q2-up1
  
    eg: grep -Hr <java home location of SJSAS7-REF>
  
    /opt/sjsas7-2004Q2-up1

  * Do a admin-server test
  
    cd $SJSAS7/domains/<domain-name>/admin-server/bin
  
    ./startserv -configtest
  * Deploy some sample application to test the instance. 

<big><big><span style="font-weight: bold;"></span></big></big>



<big><big><span style="font-weight: bold;">Conclusion</span></big></big>

<div style="margin-left: 40px;">
  If everything were done right, the<br /> admin-server can be started. Check the logs for any failure.</p> 
  
  <p>
    The user and password for admin-server are the same as SJSAS7-REF, be<br /> aware.
  </p>
  
  <p>
    After logged in, instances can be created through admin server (web<br /> interface or asadmin console)
  </p>
</div>

If you have any comments, fixes, please send a email to me: [Claudio Miranda](mailto:claudio%28@%29CLAUDIUS.com.br)

<div style="margin-left: 40px;">
</div>