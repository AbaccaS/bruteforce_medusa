# bruteforce_medusa
Nesse repositorio foi executado um brute force no DVWA e foi utilizado o medusa para acesso smbclient.
Para esse trabalho utilizamos o metaspoitable em uma maquina virtual junto do Kali Linux também virtualizado.
No primeiro momento ativamos o metaspoitable e identificamos o ip: 192.168.56.101. Em seguida acessamos o site http://192.168.56.101/dvwa/login.php
Testamos o acesso com um login e senha aleatorio e nos retornou falha de acesso.
Entao criamos uma wordlist de usuarios e senhas através do comando echo, apos criado essas worlist acessamos o medusa com o seguinte codigo:
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M http
-M PAGE: '/dvwa/login.php'
-m FORM: 'username=^User^&password=^PASS^&Login=Login'
-m "FAIL=Login failed' -td
Após executar esse comando o medusa correu nossa wordlist até identificar o usuario e senha que nos dão acesso ao site.

SMB PASSWORD SPRAYING
Nesse proximo teste executamos uma enumeração de usuarios e ja salvamos como .txt atravez do comando:
enum4linux -a 192.168.56.101 | tee enum4_output.txt
Com acesso a lista de usuarios que detectamos atravez dessa enumeração podemos criar uma wordlist com possiveis usuarios e senhas, após criada essas wordlist podemos rodar o medusa através do seguinte código:
medusa -h 192.168.56.101 -U smb_users.txt -P senhas_spray.txt -M smbnt -t 2 -T 50
Esse codigo nos retornou varias tentativas de acesso com a lista de usuarios e senhas ate dar uma mensagem de sucesso onde encontro o usuario e senha correspondente ao acesso do smbclient
