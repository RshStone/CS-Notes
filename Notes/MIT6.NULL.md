# Shell Tools and Scripting

space, "" need to be careful.  "", '' may be equal but other cases are not.

```shell
echo "Value is $foo"
echo 'Value is $foo'

true
echo $?

false
echo $?

false ; echo "This will always print"   (;concatenate)

cat < (ls) < (ls ..)

$0 the file name that we are openning
$$ process ID of the command line are running
$@ expanding to all arguments
$# 
$?
$file

*.sh
ls project?

image.{png,jpg}

fing . -name src -type d
find . -path '**/test/*.py' -type f

find stuff and do stuff
find . -name "*.tmp" -exec rm {}\


```

 Kayid Theme

`dpkg -L <packagename>`

`sudo apt-get install <app>`. After that, where the software should be laid? 

[After doing a sudo apt-get install , where does the application get stored to? [duplicate\]](https://askubuntu.com/questions/408784/after-doing-a-sudo-apt-get-install-app-where-does-the-application-get-stored)





### Ubuntu System

1. 7 Hier

   

   [How to understand the Ubuntu file system layout?](https://askubuntu.com/questions/138547/how-to-understand-the-ubuntu-file-system-layout)

   ![https://i.stack.imgur.com/BlpRb.png](https://i.stack.imgur.com/BlpRb.png)

2. 1

   