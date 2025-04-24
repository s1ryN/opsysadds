# opsysadds
1.	Instalace windows
2.	Instalace virtualbox
3.	Instalace WinServeru a Win10 do virtualboxu (skip unattended installation u serveru pro desktop experience)
4.	U serveru vybrat “Standard (Desktop Experience)” a nic neupgradovat (Custom installation)
5.	Radši u Windows 10 změnit MAC adresu (síťová nastavení ve virtualboxu)
6.	Všechno dát do NAT network, začít od xxx.xxx.xxx.10 a dál (NAT ve virtualboxu) (Udělat ve VIRTUALBOXU vlastní NAT síť a zakázat v ní DHCP)
7.	Až se dostaneme do Windowsů, změnit HOSTNAME na něco normálního co není random
8.	IP adresy v síti dělat až třeba po 10 prvních adresách, protože virtual
9.	Nastavit u serveru IP na NAT síť, pak gateway na první adresu v NAT síti a DNS u serveru na sebe 
10.	U Win10 nastavit IP na další IP adresu v NAT síti, pak gateway na server a DNS taky na server
11.	U Win10 aktivovat administrátora (přes pravé kliknutí na dolní logo windows -> správa počítače -> uživatelé a skupiny -> uživatelé -> otevřít administrátora a aktivovat ho -> změnit mu heslo na něco co se dobře pamatuje)
12.	Na serveru přes AD začneme stavit doménu přes Manage -> Add Roles and Features -> Server Roles (na nic předtím nehrabat) -> aktivovat Active Directory Domain Services; DNS server; pod File and Storage Services rozklikat a najít File Server + File Server Resource Manager)
13.	Dáme instalovat a zaklikneme mu “Restart if needed”
14.	Následně se v server manager objeví vlaječka s vykřičníkem, kde dáme “Promote this server to domain controller” a poté dáme “Add a new forest”, pojmenujeme doménu a pak zadáme v dalším poli heslo pro Recovery, poté nám to vytváří doménu a její jméno z našeho zadaného (něco.něco), dale už jen skipujeme až do další instalace
15.	Pak pro přidání uživatele do domény se přihlásit na klasických Win10 pod admistrátorem, proklikat se v nastavení do změny jména (nastavení -> o aplikaci -> přejmenovat tento počítač (dole nebo na straně) -> název počítače -> změnit -> je členem)
16.	V doméně do users (Active Directory Users and Computers) přidáváme skupiny a uživatele do těchto skupin (rightclick na jméno domény -> new -> organization unit)
17.	V Group Policy Management nastavíme nová pravidla a následně je nalinkuje (rightclick na Group Policy Objects-> New / nebo rightclick na skupinu -> Create a GPO in this domain and Link it here…) a poté přes další right click na organization unity můžeme vytvořené Policies nalinkovat (rightclick na skupinu -> Link an existing GPO…) 
18.	BONUS – DHCP – pevné adresy nesmí být částí rozsahu DHCP serveru – server manager -> Tools -> DHCP -> rightclick na IPv4 -> New scope -> po pár kliknutí nastavíme defaultní router na server (instalace přes Manage -> Add roles and feature -> Server roles -> DHCP)
19.	Poté shared folder – na disku C: našeho serveru vytvoříme složku určenou pro sdílení 
20.	Otevřeme tools -> Active Directory Users and Computers -> rightclick na Users -> New -> Group -> přidat jméno -> následně rozklikneme Users, najdeme skupinu a rozklikneme -> Members -> Add… -> najdeme uživatele podle jména a přidáme
21.	Následně na složku dáme rightclick -> Properties -> Security -> přidáme naše 2 skupiny (Edit -> Add…), odstraníme skupinu Users (Edit -> Remove), vypneme dědičnost (Advanced -> Disable inheritance) a zkontrolujeme pravidla pro dané skupiny, které přes Edit -> Permissions for jmenoskupiny a dolní okénka (zároveň také přes Properties -> Sharing -> Advanced Sharing -> Permissions můžeme práva donastavit (méně okének))
