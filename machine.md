<h1> Tryhackme Magician Machine </h1>
<h3>by purpler0se</h3>
	<p>...enjoy :D</p>
<h2> Starting off with basic enumeration to get our ports </h2>
	<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/nmap.png">
	<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/etc.png">
	<h4> Now remembering what was instructed in the info for task one which was "Please add the IP address of this machine with the hostname 'magician'
		to your /etc/hosts file on linux before you start." (example above)</h4>
<h3> I checked out ftp port logging in as "anonymous" user with no password</h3><h4> ftp [MACHINE_IP] 21 </h4>
	<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/ftp.png">
<h3> I got prompted with this as i logged in. It told me a clue that will help us later in our payload</h3>
	</h4>https://imagetragick.com</h4>
</br>
<h1>Web enumeration</h1>
	<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/convert.png">

<h3> Port 8081 had a png to jpg converted which could be a ticket for our shell</h3>
	<h4>but port 8080,for now had nothing intresting</h4>
	<h3> with that given link (https://imagetragick.com) we can create a reverse shell payload</h3>
</br>
<h1> Creating mv Png Payload </h2>
	<h3>On you local machine run these commands</h3>
		<h4>touch reverse.png</h4>
		<h4> nano reverse.png</h4>
	<h3>Paste this code in</h3>
		<h4></h4>
		<h3>I've changed the original payload at https://imagetragick.com so it gives us a shell, further explaination of this exploit CVE-2016-3174 at https://imagetragick.com</h3></br>
			<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/payload.png">
		<h4>Your payload should look like this</h4>
<h1> Getting a shell</h1>
	<h3>Setup a netcat listner on your local machine</h3>
	<h4> nc -lnvp [any_port]</h4>
		<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/upload.png">
	<h3> Now upload that payload and onces its submitted click on it and then just wait for a callback</h3>
		<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/shell.png">
	<h3>Once you get the callback upgrade your shell by doing the following commands</h3>
	<h4>export TERM=xterm</h4>
	<h4>python3 -c "import pty;pty.spawn('/bin/bash')"</h4>
	<h4>CTRL + Z</h4>
	<h4>BASH: stty raw -echo && fg</br>
	ZSH: stty raw -echo; fg
	</h4>
	<h4> and then WHACK your enter key 3x</h4>
	<h4> stty rows [yours] cols [yours] (You can find your rows and columns by doing stty -a on your local machine</h4>
<h1> From Magician to ROOT</h1>
		<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/hint.png">
	<h3>We got a hint in the home directory magician, file named "the_magic_continues," the giveaway to the priv esc is "locally listening" therefore its a internal ip priv esc 			situation.We can list the listening connection on the targets machine by doing</h3>
	<h4>netstat -ant</h4>
		<img src="https://github.com/purpler0se/tryhackme-writeups/blob/main/images/ips.png">
	<h3>As you can see the localhost on port 6666 is listening. I did the following command</h3>
		<h4> curl 127.0.0.1:6666</h4>
	<h3>And got the code for a simple input website - i think was suppose to be port 8081</h3>
	<h3>Now reading the source code u can see there is a input with the name "filename" so the code i used to send to this input is</h3>
		<h4>curl --request POST 'http://127.0.0.1:6666' --data "filename=/root/root.txt"</h4>
	<h3>I decrypted this by going to https://gchq.github.io/CyberChef/ and using the "From Hex" to get the THM{} flag</h3>
<h2>Socials</h2>
discord - purpler0se#6981
tryhackme - https://tryhackme.com/p/purplerose
<h1> Thanks for reading my writeup on how i tackled this machine</h1>
	
	
	
	
