#!/bin/bash
#script pra minerar xmr ( monero ) pool suportado MINERGATE E SUPPORTXMR
supportxmr(){
	echo
	echo -e "\033[1;32mPARA CONTINUAR COLOQUE SUA CARTEIRA DA SUPPORTXMR\nEX:\033[1;31m 48GzSehCFey5TkbVWHBdSu4G5CCLP2V6C7DmYXqJhBDncWTYUyHrGZ8hRfdoFb5xRmRh9xQPNg3dMYH27m32r9Dq6RnUvLL\033[1;33m"
	echo
	read -p "Carteira: " supports
	echo -e "\033[0m"
	screen -dmS screen ./minerd -a cryptonight -o stratum+tcp://at02.supportxmr.com:3333 -p ${supports} -t 5
	echo "\033[1;37m Finalizado. jÃ¡ esta minerando\nPara acompanhar a mineraÃ§Ã£o use o comando ( screen -r ) \033[0m"
	echo 'supportxmr' > /etc/instalado
	exit
}
minergate(){
	echo
	echo -e "\033[1;32mPARA CONTINUAR COLOQUE SEU E-MAIL DA MINERGATE\nEX:\033[1;31m seu.email@gmail.com ou otros modelo de e-mail\033[1;33m"
	echo
	read -p "Carteira: " minergates
	echo -e "\033[0m"
	screen -dmS screen minerd -a cryptonight -o stratum+tcp://xmr.pool.minergate.com:45560 -u ${minergates} -p x
	echo "\033[1;37m Finalizado. jÃ¡ esta minerando\nPara acompanhar a mineraÃ§Ã£o use o comando ( screen -r ) \033[0m"
	echo 'minergate' > /etc/instalado
	exit
}
if [[ -e "/etc/instalado" ]]
 then
clear
echo -e "\033[1;31mOPSS,\033[1;32mSEU SERVIDOR JA ESTA CONFIGURADO E MINERANDO"
echo -e "Deseja reinicia a screen caso tenha parado?"
read -p "[Y/N]: " OSS
case $OSS in
(y|Y)
echo -e "\033[1;32m[ ok ]"
sleep 2
;;
*)
echo -e "\033[1;31mSAINDO..\033[0m"
rm install_xmr
exit
;;
esac
CAXMR=$(cat /etc/instalado)
echo -e "\033[1;37mSUA CARTEIRA Ã‰ DA \033[1;32m${CAXMR}\033[0m"
${CAXMR}
else
sudo apt-get upgrade -y > /dev/null 2>&1
sudo apt-get update -y > /dev/null 2>&1
sudo apt-get install figlet -y > /dev/null 2>&1
sudo apt-get install screen -y > /dev/null 2>&1
sudo apt-get install git -y > /dev/null 2>&1
sudo apt-get install build-essential autotools-dev autoconf libcurl3 libcurl4-gnutls-dev -y > /dev/null 2>&1
git clone https://github.com/OhGodAPet/cpuminer-multi > /dev/null 2>&1
cd cpuminer-multi/
chmod +x autogen.sh
./autogen.sh > /dev/null 2>&1
CFLAGS="-march=native" ./configure > /dev/null 2>&1
make > /dev/null 2>&1
sudo make install -y > /dev/null 2>&1
echo -e "\033[1;36m"
figlet miner XMR
menu() {
	clear
	echo -e "\033[1;31mQual a sua pool ?\033[1;35"
	echo -e "------------------------------------------"
	echo -e "\033[1;32m[ 1 ] -- \033[1;33m|  MINERGATE |"
	echo -e "\033[1;32m[ 2 ] -- \033[1;33m| SUPPORTXMR |\033[1;37m"
	read -p "Qual ?: " decide
	case ${decide} in
		1) supportxmr ;;
		2) minergate ;;
		*) "nenhuma opÃ§Ã£o selecionada" ; echo ; menu ;;
	esac
}
fi
clear
exit


