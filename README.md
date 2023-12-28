# WkhtmlToPdfMigration
There is good solution for convert html data to pdf known as Wkhtmltopdf https://wkhtmltopdf.org/ and there is .NET wrapper for this library https://github.com/HakanL/WkHtmlToPdf-DotNet .
Once our team faced with issue linked to this wrapper. It works good on Windows platform and throwing exception on Linux platform despite the stated support linux.
Exception like this:
System.NotSupportedException : Unable to load native library. The platform may be missing native dependencies (libjpeg62, etc). Or the current platform is not supported.
It was really simple to install libjpeg62 library, but issue remained unresolved.
What about look at all dependencies of wkhtmltopdf 0.12.5? All of them are already installed.
What about change wkhtmltopdf version? Done. All of required dependencies are installed. 
What about look at dependencies oflibjpeg62? Already installed, again.
After that I found this topic - https://github.com/HakanL/WkHtmlToPdf-DotNet/issues/64 where folks talked about additional libraries.
Eventually, after many hours we had collected info from many topics and got list of required libraries and installations:

1. sudo rpm -i wkhtmltox-0.12.6-1.centos7.x86_64.rpm
2. yum install libpng.so.3
3. yum install libpng15.so.15
4. yum install -y openssl-devel
-yum install libjpeg-turbo
-yum install libgdiplus.so
-yum install libpng15.so.15
-yum install -y libpng12.x86_64
-yum install -y libpng15.x86_64
-yum install xorg-x11-fonts-75dpi
-yum install libgdiplus
-yum install libjpeg

It was verified on RedOS7, CentOS7, AlmaLinux, RHEL7.
For 8th versions it works too with adjustments for package versions and their dependencies certainly.
For example 8th version should be installed via sudo rpm -i wkhtmltox-0.12.6.1-2.almalinux8.x86_64.rpm

I hope it can save a few hours in your life)

