---
title: Wiimote y Bluetooth
author: laparca
type: post
date: 2007-01-07T13:10:38+00:00
url: /2007/01/07/wiimote-y-bluetooth/
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:10011:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    </pre></td><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #993333;">static</span> <span style="color: #993333;">int</span> search_wiimotes<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
        inquiry_info <span style="color: #339933;">*</span>ii <span style="color: #339933;">=</span> NULL<span style="color: #339933;">;</span>
        <span style="color: #993333;">int</span> max_rsp<span style="color: #339933;">,</span> num_rsp<span style="color: #339933;">;</span>
        <span style="color: #993333;">int</span> dev_id<span style="color: #339933;">,</span> sock<span style="color: #339933;">,</span> len<span style="color: #339933;">,</span> flags<span style="color: #339933;">;</span>
        <span style="color: #993333;">int</span> i<span style="color: #339933;">;</span>
        <span style="color: #993333;">char</span> addr<span style="color: #009900;">&#91;</span><span style="color: #0000dd;">19</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
        <span style="color: #993333;">char</span> name<span style="color: #009900;">&#91;</span><span style="color: #0000dd;">248</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    &nbsp;
        dev_id <span style="color: #339933;">=</span> hci_get_route<span style="color: #009900;">&#40;</span>NULL<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        sock <span style="color: #339933;">=</span> hci_open_dev<span style="color: #009900;">&#40;</span> dev_id <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span>dev_id <span style="color: #339933;">&lt;</span> <span style="color: #0000dd;">0</span> <span style="color: #339933;">||</span> sock <span style="color: #339933;">&lt;</span> <span style="color: #0000dd;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000066;">perror</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;opening socket&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000066;">exit</span><span style="color: #009900;">&#40;</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        len  <span style="color: #339933;">=</span> <span style="color: #0000dd;">4</span><span style="color: #339933;">;</span>
        max_rsp <span style="color: #339933;">=</span> <span style="color: #0000dd;">255</span><span style="color: #339933;">;</span>
        flags <span style="color: #339933;">=</span> IREQ_CACHE_FLUSH<span style="color: #339933;">;</span>
        ii <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>inquiry_info<span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span><span style="color: #000066;">malloc</span><span style="color: #009900;">&#40;</span>max_rsp <span style="color: #339933;">*</span> <span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>inquiry_info<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        num_rsp <span style="color: #339933;">=</span> hci_inquiry<span style="color: #009900;">&#40;</span>dev_id<span style="color: #339933;">,</span> len<span style="color: #339933;">,</span> max_rsp<span style="color: #339933;">,</span> NULL<span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span>ii<span style="color: #339933;">,</span> flags<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> num_rsp <span style="color: #339933;">&lt;</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#41;</span> <span style="color: #000066;">perror</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;hci_inquiry&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #b1b100;">for</span> <span style="color: #009900;">&#40;</span>i <span style="color: #339933;">=</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> num_rsp<span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            ba2str<span style="color: #009900;">&#40;</span><span style="color: #339933;">&amp;</span><span style="color: #009900;">&#40;</span>ii<span style="color: #339933;">+</span>i<span style="color: #009900;">&#41;</span><span style="color: #339933;">-&gt;</span>bdaddr<span style="color: #339933;">,</span> addr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000066;">memset</span><span style="color: #009900;">&#40;</span>name<span style="color: #339933;">,</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">,</span> <span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>name<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span>hci_read_remote_name<span style="color: #009900;">&#40;</span>sock<span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span><span style="color: #009900;">&#40;</span>ii<span style="color: #339933;">+</span>i<span style="color: #009900;">&#41;</span><span style="color: #339933;">-&gt;</span>bdaddr<span style="color: #339933;">,</span> <span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>name<span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> name<span style="color: #339933;">,</span> <span style="color: #0000dd;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&lt;</span> <span style="color: #0000dd;">0</span><span style="color: #009900;">&#41;</span>
    	        <span style="color: #000066;">strcpy</span><span style="color: #009900;">&#40;</span>name<span style="color: #339933;">,</span> <span style="color: #ff0000;">&quot;[unknown]&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> <span style="color: #339933;">!</span><span style="color: #000066;">strcmp</span><span style="color: #009900;">&#40;</span> name<span style="color: #339933;">,</span> <span style="color: #ff0000;">&quot;Nintendo RVL-CNT-01&quot;</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            	<span style="color: #000066;">strcpy</span><span style="color: #009900;">&#40;</span> _wii_handlers<span style="color: #009900;">&#91;</span>_wii_counter<span style="color: #009900;">&#93;</span>.<span style="color: #202020;">addr</span><span style="color: #339933;">,</span> addr <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            	_wii_counter <span style="color: #339933;">++;</span>
            <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000066;">free</span><span style="color: #009900;">&#40;</span> ii <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        close<span style="color: #009900;">&#40;</span> sock <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #b1b100;">return</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">static int search_wiimotes()
    {
        inquiry_info *ii = NULL;
        int max_rsp, num_rsp;
        int dev_id, sock, len, flags;
        int i;
        char addr[19] = { 0 };
        char name[248] = { 0 };
    
        dev_id = hci_get_route(NULL);
        sock = hci_open_dev( dev_id );
        if (dev_id &lt; 0 || sock &lt; 0) {
            perror(&quot;opening socket&quot;);
            exit(1);
        }
    
        len  = 4;
        max_rsp = 255;
        flags = IREQ_CACHE_FLUSH;
        ii = (inquiry_info*)malloc(max_rsp * sizeof(inquiry_info));
        
        num_rsp = hci_inquiry(dev_id, len, max_rsp, NULL, &amp;ii, flags);
        if( num_rsp &lt; 0 ) perror(&quot;hci_inquiry&quot;);
    
        for (i = 0; i &lt; num_rsp; i++) {
            ba2str(&amp;(ii+i)-&gt;bdaddr, addr);
            memset(name, 0, sizeof(name));
            if (hci_read_remote_name(sock, &amp;(ii+i)-&gt;bdaddr, sizeof(name), name, 0) &lt; 0)
    	        strcpy(name, &quot;[unknown]&quot;);
            if( !strcmp( name, &quot;Nintendo RVL-CNT-01&quot; ) ) {
            	strcpy( _wii_handlers[_wii_counter].addr, addr );
            	_wii_counter ++;
            }
        }
    
        free( ii );
        close( sock );
        
        return 0;
    }</p></div>
    ";i:2;s:8741:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    </pre></td><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/**
     * Crea una conexión con un wiimote.
     * @param addr Dirección del wiimote
     */</span>
    <span style="color: #993333;">static</span> <span style="color: #993333;">int</span> wii_internal_connect<span style="color: #009900;">&#40;</span> <span style="color: #993333;">char</span> addr<span style="color: #009900;">&#91;</span><span style="color: #0000dd;">19</span><span style="color: #009900;">&#93;</span> <span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    	<span style="color: #993333;">struct</span> sockaddr_l2 loc_addr<span style="color: #339933;">;</span>
    	<span style="color: #993333;">int</span> fd_in<span style="color: #339933;">,</span> fd_out<span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #000066;">fprintf</span><span style="color: #009900;">&#40;</span> stderr<span style="color: #339933;">,</span> <span style="color: #ff0000;">&quot;Conectando a: %s<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #339933;">,</span> addr <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    	fd_in <span style="color: #339933;">=</span> socket<span style="color: #009900;">&#40;</span> AF_BLUETOOTH<span style="color: #339933;">,</span> SOCK_SEQPACKET<span style="color: #339933;">,</span> BTPROTO_L2CAP <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> fd_in <span style="color: #339933;">&lt;</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#41;</span> <span style="color: #b1b100;">return</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #339933;">;</span>
    &nbsp;
    	str2ba<span style="color: #009900;">&#40;</span> addr<span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span>loc_addr.<span style="color: #202020;">l2_bdaddr</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	loc_addr.<span style="color: #202020;">l2_family</span> <span style="color: #339933;">=</span> AF_BLUETOOTH<span style="color: #339933;">;</span>
    	loc_addr.<span style="color: #202020;">l2_psm</span> <span style="color: #339933;">=</span> htobs<span style="color: #009900;">&#40;</span> <span style="color: #208080;">0x13</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> connect<span style="color: #009900;">&#40;</span> fd_in<span style="color: #339933;">,</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">struct</span> sockaddr <span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">&amp;</span>loc_addr<span style="color: #339933;">,</span> <span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>loc_addr<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #339933;">&lt;</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		close<span style="color: #009900;">&#40;</span> fd_in <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #b1b100;">return</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	fd_out <span style="color: #339933;">=</span> socket<span style="color: #009900;">&#40;</span> AF_BLUETOOTH<span style="color: #339933;">,</span> SOCK_SEQPACKET<span style="color: #339933;">,</span> BTPROTO_L2CAP <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> fd_out <span style="color: #339933;">&lt;</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		close<span style="color: #009900;">&#40;</span> fd_in <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #b1b100;">return</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	str2ba<span style="color: #009900;">&#40;</span> addr<span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span>loc_addr.<span style="color: #202020;">l2_bdaddr</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	loc_addr.<span style="color: #202020;">l2_family</span> <span style="color: #339933;">=</span> AF_BLUETOOTH<span style="color: #339933;">;</span>
    	loc_addr.<span style="color: #202020;">l2_psm</span> <span style="color: #339933;">=</span> htobs<span style="color: #009900;">&#40;</span> <span style="color: #208080;">0x11</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> connect<span style="color: #009900;">&#40;</span> fd_out<span style="color: #339933;">,</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">struct</span> sockaddr <span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">&amp;</span>loc_addr<span style="color: #339933;">,</span> <span style="color: #993333;">sizeof</span><span style="color: #009900;">&#40;</span>loc_addr<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #339933;">&lt;</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		close<span style="color: #009900;">&#40;</span> fd_out <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		close<span style="color: #009900;">&#40;</span> fd_in <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #b1b100;">return</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    &nbsp;
    	_wii_handlers<span style="color: #009900;">&#91;</span>_wii_counter<span style="color: #009900;">&#93;</span>.<span style="color: #202020;">in</span>  <span style="color: #339933;">=</span> fd_in<span style="color: #339933;">;</span>
    	_wii_handlers<span style="color: #009900;">&#91;</span>_wii_counter<span style="color: #009900;">&#93;</span>.<span style="color: #202020;">out</span> <span style="color: #339933;">=</span> fd_out<span style="color: #339933;">;</span>
    	_wii_counter <span style="color: #339933;">++;</span>
    &nbsp;
    	<span style="color: #b1b100;">return</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
     * Crea una conexión con un wiimote.
     * @param addr Dirección del wiimote
     */
    static int wii_internal_connect( char addr[19] )
    {
    	struct sockaddr_l2 loc_addr;
    	int fd_in, fd_out;
    	
    	fprintf( stderr, &quot;Conectando a: %s\n&quot;, addr );
    	
    	fd_in = socket( AF_BLUETOOTH, SOCK_SEQPACKET, BTPROTO_L2CAP );
    	if( fd_in &lt; 0 ) return -1;
    
    	str2ba( addr, &amp;loc_addr.l2_bdaddr );
    	loc_addr.l2_family = AF_BLUETOOTH;
    	loc_addr.l2_psm = htobs( 0x13 );
    	
    	if( connect( fd_in, (struct sockaddr *)&amp;loc_addr, sizeof(loc_addr) ) &lt; 0 ) {
    		close( fd_in );
    		return -1;
    	}
    
    	fd_out = socket( AF_BLUETOOTH, SOCK_SEQPACKET, BTPROTO_L2CAP );
    	if( fd_out &lt; 0 ) {
    		close( fd_in );
    		return -1;
    	}
    
    	str2ba( addr, &amp;loc_addr.l2_bdaddr );
    	loc_addr.l2_family = AF_BLUETOOTH;
    	loc_addr.l2_psm = htobs( 0x11 );
    	
    	if( connect( fd_out, (struct sockaddr *)&amp;loc_addr, sizeof(loc_addr) ) &lt; 0 ) {
    		close( fd_out );
    		close( fd_in );
    		return -1;
    	}
    
    	
    	_wii_handlers[_wii_counter].in  = fd_in;
    	_wii_handlers[_wii_counter].out = fd_out;
    	_wii_counter ++;
    	
    	return 0;
    }</p></div>
    ";}
categories:
  - Desarrollo
  - Personal

---
Como comenta [Queltosh][1], estamos trabajando en programar desde linux el mando de la Nintendo Wii. De momento tengo varias cositas hechas, pero de poca importancia, principalmente la detección y conexión de los mandos que halla. La siguiente porción de código es la que se encarga de la detección:

<pre lang="c" line="1">static int search_wiimotes()
{
    inquiry_info *ii = NULL;
    int max_rsp, num_rsp;
    int dev_id, sock, len, flags;
    int i;
    char addr[19] = { 0 };
    char name[248] = { 0 };

    dev_id = hci_get_route(NULL);
    sock = hci_open_dev( dev_id );
    if (dev_id &lt; 0 || sock &lt; 0) {
        perror("opening socket");
        exit(1);
    }

    len  = 4;
    max_rsp = 255;
    flags = IREQ_CACHE_FLUSH;
    ii = (inquiry_info*)malloc(max_rsp * sizeof(inquiry_info));
    
    num_rsp = hci_inquiry(dev_id, len, max_rsp, NULL, &#038;ii, flags);
    if( num_rsp &lt; 0 ) perror("hci_inquiry");

    for (i = 0; i &lt; num_rsp; i++) {
        ba2str(&#038;(ii+i)->bdaddr, addr);
        memset(name, 0, sizeof(name));
        if (hci_read_remote_name(sock, &(ii+i)->bdaddr, sizeof(name), name, 0) &lt; 0)
	        strcpy(name, "[unknown]");
        if( !strcmp( name, "Nintendo RVL-CNT-01" ) ) {
        	strcpy( _wii_handlers[_wii_counter].addr, addr );
        	_wii_counter ++;
        }
    }

    free( ii );
    close( sock );
    
    return 0;
}
</pre>

Con el código anterior se detectan hasta un máximo de 255 dispositivos Bluetooth y luego seleccionamos los que sean Wiimotes. 

Una vez hemos detectado todos los Wiimotes, procedemos a conectarnos a ellos. Pues en este punto surje un problema: algunas implementaciones de la biblioteca Bluez (o de la pila de Bluetooth, no estoy seguro), tienen un fallo y no dejan realizar la conexión, diciendo que la clave no es correcta. Parece ser que el fallo ya está solucionado en versiones posteriores, pero en la que trae Ubutu Edgy (la que uso para las pruebas) no :'(. Así que a esperar toca.

Para los que quieran el código que hace la conexión con un Wiimote:

<pre lang="c" line="1">/**
 * Crea una conexión con un wiimote.
 * @param addr Dirección del wiimote
 */
static int wii_internal_connect( char addr[19] )
{
	struct sockaddr_l2 loc_addr;
	int fd_in, fd_out;
	
	fprintf( stderr, "Conectando a: %s\n", addr );
	
	fd_in = socket( AF_BLUETOOTH, SOCK_SEQPACKET, BTPROTO_L2CAP );
	if( fd_in &lt; 0 ) return -1;

	str2ba( addr, &#038;loc_addr.l2_bdaddr );
	loc_addr.l2_family = AF_BLUETOOTH;
	loc_addr.l2_psm = htobs( 0x13 );
	
	if( connect( fd_in, (struct sockaddr *)&#038;loc_addr, sizeof(loc_addr) ) &lt; 0 ) {
		close( fd_in );
		return -1;
	}

	fd_out = socket( AF_BLUETOOTH, SOCK_SEQPACKET, BTPROTO_L2CAP );
	if( fd_out &lt; 0 ) {
		close( fd_in );
		return -1;
	}

	str2ba( addr, &#038;loc_addr.l2_bdaddr );
	loc_addr.l2_family = AF_BLUETOOTH;
	loc_addr.l2_psm = htobs( 0x11 );
	
	if( connect( fd_out, (struct sockaddr *)&#038;loc_addr, sizeof(loc_addr) ) &lt; 0 ) {
		close( fd_out );
		close( fd_in );
		return -1;
	}

	
	_wii_handlers[_wii_counter].in  = fd_in;
	_wii_handlers[_wii_counter].out = fd_out;
	_wii_counter ++;
	
	return 0;
}
</pre>

 [1]: http://queltosh.blogspot.com/2006/12/wiimote.html