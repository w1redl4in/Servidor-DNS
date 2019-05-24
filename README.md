# Instalação 
    sudo su
    apt install bind9 -y
    
# Configuração 
    cd /etc/bind
    cp named.local.default-zones named.conf.local
    
# Configurando named.conf.local
     vim named.conf.local
     zone"teste.local"{
        type master;
        file "/etc/bind/db.teste.local";
     };
     
# Criando db.teste.local
    cp db.local db.teste.local
    
  ## Editando db.teste.local
  ### Os pontos finais são muito importantes, não esqueça nenhum
    vim db.teste.local
    
    
    
    	$TTL	604800
	@	IN	SOA	nomedamaquina.exemplo.local.	root.exemplo.local. (
						2		;Serial
						604800		; Refresh
						86400		; Retry
						2419200		; Expire
						604800 )	; Negative Cache TTL
	;
	exemplo.local.	IN	NS	nomedamaquina.exemplo.local.
	exemplo.local.	IN	A	192.168.100.11
	nomedamaquina	IN	A	192.168.100.11
	www		IN	CNAME	exemplo.local.
    
 # named.conf.options
    Apenas retirar os comentários das linhas:
      forwarders{
          8.8.8.8;
      }
      
 # resolv.conf
    nameserver seuip
    
 # hosts
    seuip           nomedasuamaquina@exemplo.local          nomedamaquina
    
 # teste
    ping www.exemplo.local
    
 # Implementação no DHCP
##  Insira esta linha dentro do escopo de configuração do DHCP
	option domain-name-servers 192.168.100.11, 8.8.8.8;
					
    
