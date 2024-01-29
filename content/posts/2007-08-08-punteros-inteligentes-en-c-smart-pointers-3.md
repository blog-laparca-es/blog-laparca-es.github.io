---
title: Punteros inteligentes en C++ (smart pointers) 3
author: laparca
type: post
date: 2007-08-08T20:45:57+00:00
url: /2007/08/08/punteros-inteligentes-en-c-smart-pointers-3/
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:3952:"
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
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _t<span style="color: #000080;">&gt;</span> <span style="color: #0000ff;">class</span> PtrSimple2 <span style="color: #008000;">&#123;</span>
    <span style="color: #008000;">&#91;</span>..<span style="color: #008000;">&#93;</span>
       PtrSimple2<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span>
       <span style="color: #666666;">// &lt;/_t&gt;</span>
       operator<span style="color: #000080;">=</span><span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">const</span> PtrSimple2<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> ptr <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #666666;">// Hay que decrementar el puntero viejo, y en caso necesario</span>
          <span style="color: #666666;">// liberar la memoria</span>
          <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>_count<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>_count<span style="color: #008000;">&#41;</span> <span style="color: #000040;">-</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
          <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> <span style="color: #000040;">*</span>_count <span style="color: #000080;">==</span> <span style="color: #0000dd;">0</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
             <span style="color: #0000dd;">delete</span> _count<span style="color: #008080;">;</span>
             <span style="color: #0000dd;">delete</span> _ptr<span style="color: #008080;">;</span>
          <span style="color: #008000;">&#125;</span>
          _count <span style="color: #000080;">=</span> ptr._count<span style="color: #008080;">;</span>
          _ptr <span style="color: #000080;">=</span> ptr._ptr<span style="color: #008080;">;</span>
          <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>_count<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>_count<span style="color: #008000;">&#41;</span> <span style="color: #000040;">+</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
    &nbsp;
          <span style="color: #0000ff;">return</span> <span style="color: #000040;">*</span><span style="color: #0000dd;">this</span><span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#91;</span>..<span style="color: #008000;">&#93;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    <span style="color: #666666;">//&lt;/_t&gt;&lt;/typename&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">template&lt;typename _t&gt; class PtrSimple2 {
    [..]
       PtrSimple2&lt;_t&gt;&amp;
       // &lt;/_t&gt;
       operator=( const PtrSimple2&lt;_t&gt;&amp; ptr ) {
          // Hay que decrementar el puntero viejo, y en caso necesario
          // liberar la memoria
          (*_count) = (*_count) - 1;
          if( *_count == 0 ) {
             delete _count;
             delete _ptr;
          }
          _count = ptr._count;
          _ptr = ptr._ptr;
          (*_count) = (*_count) + 1;
    
          return *this;
       }
    [..]
    };
    //&lt;/_t&gt;&lt;/typename&gt;</p></div>
    ";i:2;s:7431:"
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
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _t<span style="color: #000080;">&gt;</span> <span style="color: #0000ff;">class</span> PtrSimple2 <span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">//&lt;/typename&gt;</span>
    <span style="color: #008000;">&#91;</span>..<span style="color: #008000;">&#93;</span>
    <span style="color: #0000ff;">public</span><span style="color: #008080;">:</span>
       <span style="color: #666666;">// Para poder leer el puntero sin problemas</span>
       _t<span style="color: #000040;">*</span> get_ptr<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">return</span> _ptr<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       <span style="color: #666666;">// Nuevo constructor</span>
       <span style="color: #666666;">// Estoy simplificando algunas cosas, es posible que no se pueda acceder</span>
       <span style="color: #666666;">// directamente a los miembros del otro puntero</span>
       <span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _u<span style="color: #000080;">&gt;</span> PtrSimple2<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">const</span> PtrSimple2<span style="color: #000080;">&lt;</span>_u<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> ptr <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          _count <span style="color: #000080;">=</span> ptr._count<span style="color: #008080;">;</span>
          _ptr <span style="color: #000080;">=</span> <span style="color: #0000ff;">dynamic_cast</span><span style="color: #000080;">&lt;</span>_t <span style="color: #000040;">*</span><span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span> ptr._ptr <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
          <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>count<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>count<span style="color: #008000;">&#41;</span> <span style="color: #000040;">+</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span> <span style="color: #666666;">// &lt;/_t&gt;&lt;/_u&gt;&lt;/typename&gt;</span>
    &nbsp;
       <span style="color: #666666;">// Con el operador = hay que hacer lo mismo</span>
       <span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _u<span style="color: #000080;">&gt;</span> PtrSimple2<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> operator<span style="color: #000080;">=</span><span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">const</span> PtrSimple2<span style="color: #000080;">&lt;</span>_u<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> ptr <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #666666;">// Hay que decrementar el puntero viejo, y en caso necesario</span>
          <span style="color: #666666;">// liberar la memoria</span>
          <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>_count<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>_count<span style="color: #008000;">&#41;</span> <span style="color: #000040;">-</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
          <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> <span style="color: #000040;">*</span>_count <span style="color: #000080;">==</span> <span style="color: #0000dd;">0</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
             <span style="color: #0000dd;">delete</span> _count<span style="color: #008080;">;</span>
             <span style="color: #0000dd;">delete</span> _ptr<span style="color: #008080;">;</span>
          <span style="color: #008000;">&#125;</span>
          _count <span style="color: #000080;">=</span> ptr._count<span style="color: #008080;">;</span>
          _ptr <span style="color: #000080;">=</span> <span style="color: #0000ff;">dynamic_cast</span><span style="color: #000080;">&lt;</span>_t <span style="color: #000040;">*</span><span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span> ptr._ptr <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
          <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>_count<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>_count<span style="color: #008000;">&#41;</span> <span style="color: #000040;">+</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
    &nbsp;
          <span style="color: #0000ff;">return</span> <span style="color: #000040;">*</span><span style="color: #0000dd;">this</span><span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#91;</span>..<span style="color: #008000;">&#93;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    <span style="color: #666666;">//&lt;/_t&gt;&lt;/_u&gt;&lt;/_t&gt;&lt;/typename&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">template&lt;typename _t&gt; class PtrSimple2 {
    //&lt;/typename&gt;
    [..]
    public:
       // Para poder leer el puntero sin problemas
       _t* get_ptr() {
          return _ptr;
       }
    
       // Nuevo constructor
       // Estoy simplificando algunas cosas, es posible que no se pueda acceder
       // directamente a los miembros del otro puntero
       template&lt;typename _u&gt; PtrSimple2( const PtrSimple2&lt;_u&gt;&amp; ptr ) {
          _count = ptr._count;
          _ptr = dynamic_cast&lt;_t *&gt;( ptr._ptr );
          (*count) = (*count) + 1;
       } // &lt;/_t&gt;&lt;/_u&gt;&lt;/typename&gt;
    
       // Con el operador = hay que hacer lo mismo
       template&lt;typename _u&gt; PtrSimple2&lt;_t&gt;&amp; operator=( const PtrSimple2&lt;_u&gt;&amp; ptr ) {
          // Hay que decrementar el puntero viejo, y en caso necesario
          // liberar la memoria
          (*_count) = (*_count) - 1;
          if( *_count == 0 ) {
             delete _count;
             delete _ptr;
          }
          _count = ptr._count;
          _ptr = dynamic_cast&lt;_t *&gt;( ptr._ptr );
          (*_count) = (*_count) + 1;
    
          return *this;
       }
    [..]
    };
    //&lt;/_t&gt;&lt;/_u&gt;&lt;/_t&gt;&lt;/typename&gt;</p></div>
    ";i:3;s:17442:"
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
    47
    48
    49
    50
    51
    52
    53
    54
    55
    56
    57
    58
    59
    60
    61
    62
    63
    64
    65
    66
    67
    68
    69
    70
    71
    72
    73
    74
    75
    76
    77
    78
    79
    80
    81
    82
    83
    84
    85
    86
    87
    88
    89
    90
    91
    92
    93
    94
    95
    96
    97
    98
    99
    100
    101
    102
    103
    104
    105
    106
    107
    108
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #666666;">// ESTO VA EN LA CABECERA</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> pointer_inc_ref<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">void</span> <span style="color: #000040;">*</span>ptr <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">bool</span> pointer_dec_ref<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">void</span> <span style="color: #000040;">*</span>ptr <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/**
     * Creates a smart pointer type that can free the memory used
     * automatically when it isn't necesary.
     * This pointer type can be very slow.
     */</span>
    <span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _t<span style="color: #000080;">&gt;</span> <span style="color: #0000ff;">class</span> pointer_to <span style="color: #008000;">&#123;</span>
    	Type <span style="color: #000040;">*</span>ptr<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">public</span><span style="color: #008080;">:</span>
    	pointer_to<span style="color: #008000;">&#40;</span> _t <span style="color: #000040;">*</span>pointer <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		ptr <span style="color: #000080;">=</span> pointer<span style="color: #008080;">;</span>
    		pointer_inc_ref<span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	pointer_to<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">const</span> pointer_to<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> pointer <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		ptr <span style="color: #000080;">=</span> pointer.<span style="color: #007788;">ptr</span><span style="color: #008080;">;</span>
    		pointer_inc_ref<span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	<span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _u<span style="color: #000080;">&gt;</span> pointer_to<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">const</span> pointer_to<span style="color: #000080;">&lt;</span>_u<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> pointer <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		ptr <span style="color: #000080;">=</span> <span style="color: #0000ff;">dynamic_cast</span><span style="color: #000080;">&lt;</span>_t <span style="color: #000040;">*</span><span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span> pointer.<span style="color: #007788;">get</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    		pointer_inc_ref<span style="color: #008000;">&#40;</span> ptr <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	~pointer_to<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> pointer_dec_ref<span style="color: #008000;">&#40;</span> ptr <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#41;</span>
    			<span style="color: #0000dd;">delete</span> ptr<span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	_t<span style="color: #000040;">*</span> get<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span> <span style="color: #008000;">&#123;</span>
    		<span style="color: #0000ff;">return</span> ptr<span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	_t<span style="color: #000040;">*</span> operator<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span> <span style="color: #008000;">&#123;</span>
    		<span style="color: #0000ff;">return</span> ptr<span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	_t<span style="color: #000040;">&amp;</span> operator<span style="color: #000040;">*</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span> <span style="color: #008000;">&#123;</span>
    		<span style="color: #0000ff;">return</span> <span style="color: #000040;">*</span>ptr<span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	<span style="color: #666666;">// &lt;/_t&gt;</span>
    	pointer_to<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> <span style="color: #666666;">// &lt;/_t&gt;</span>
    	operator<span style="color: #000080;">=</span><span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">const</span> pointer_to<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> pointer <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		<span style="color: #666666;">// &lt;/_t&gt;</span>
    		<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> pointer_dec_ref<span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#41;</span>
    			<span style="color: #0000dd;">delete</span> ptr<span style="color: #008080;">;</span>
    		ptr <span style="color: #000080;">=</span> pointer.<span style="color: #007788;">ptr</span><span style="color: #008080;">;</span>
    		pointer_inc_ref<span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	pointer_to<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> operator<span style="color: #000080;">=</span><span style="color: #008000;">&#40;</span> _t<span style="color: #000040;">*</span>pointer <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> pointer_dec_ref<span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#41;</span>
    			<span style="color: #0000dd;">delete</span> ptr<span style="color: #008080;">;</span>
    		ptr <span style="color: #000080;">=</span> pointer<span style="color: #008080;">;</span>
    		pointer_inc_ref<span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    		<span style="color: #0000ff;">return</span> <span style="color: #000040;">*</span><span style="color: #0000dd;">this</span><span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    &nbsp;
    	<span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _u<span style="color: #000080;">&gt;</span> pointer_to<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> operator<span style="color: #000080;">=</span><span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">const</span> pointer_to<span style="color: #000080;">&lt;</span>_u<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> pointer <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> pointer_dec_ref<span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#41;</span>
    			<span style="color: #0000dd;">delete</span> ptr<span style="color: #008080;">;</span>
    		ptr <span style="color: #000080;">=</span> <span style="color: #0000ff;">dynamic_cast</span><span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span> pointer.<span style="color: #007788;">ptr</span> <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    		pointer_inc_ref<span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    		<span style="color: #0000ff;">return</span> <span style="color: #000040;">*</span><span style="color: #0000dd;">this</span><span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span> <span style="color: #666666;">// class pointer_to</span>
    <span style="color: #666666;">// &lt;/_t&gt;&lt;/_u&gt;&lt;/_t&gt;&lt;/typename&gt;&lt;/_t&gt;&lt;/_u&gt;&lt;/typename&gt;&lt;/_t&gt;&lt;/typename&gt;</span>
    &nbsp;
    &nbsp;
    <span style="color: #666666;">// ESTO VA EN EL CODIGO</span>
    &nbsp;
    <span style="color: #0000ff;">typedef</span> map<span style="color: #000080;">&lt;</span><span style="color: #0000ff;">void</span> <span style="color: #000040;">*</span>, <span style="color: #0000ff;">int</span><span style="color: #000080;">&gt;</span> pointer_map_t<span style="color: #008080;">;</span>
    <span style="color: #0000ff;">typedef</span> pointer_map_t<span style="color: #008080;">::</span><span style="color: #007788;">iterator</span> pointer_map_iterator<span style="color: #008080;">;</span>
    <span style="color: #666666;">//&lt;/void&gt;</span>
    <span style="color: #0000ff;">static</span> map<span style="color: #000080;">&lt;</span><span style="color: #0000ff;">void</span> <span style="color: #000040;">*</span>, <span style="color: #0000ff;">int</span><span style="color: #000080;">&gt;</span> pointer_map<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> pointer_inc_ref<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">void</span> <span style="color: #000040;">*</span>ptr <span style="color: #008000;">&#41;</span>
    <span style="color: #008000;">&#123;</span>
    	<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> ptr <span style="color: #000040;">!</span><span style="color: #000080;">=</span> <span style="color: #0000dd;">0</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		pointer_map_iterator it<span style="color: #008080;">;</span>
    		it <span style="color: #000080;">=</span> pointer_map.<span style="color: #007788;">find</span><span style="color: #008000;">&#40;</span> ptr <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    		<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> it <span style="color: #000080;">==</span> pointer_map.<span style="color: #007788;">end</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    			pointer_map.<span style="color: #007788;">insert</span><span style="color: #008000;">&#40;</span>pointer_map_t<span style="color: #008080;">::</span><span style="color: #007788;">value_type</span><span style="color: #008000;">&#40;</span>ptr, <span style="color: #0000dd;">1</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    		<span style="color: #008000;">&#125;</span>
    		<span style="color: #0000ff;">else</span> <span style="color: #008000;">&#123;</span>
    			pointer_map<span style="color: #008000;">&#91;</span>ptr<span style="color: #008000;">&#93;</span> <span style="color: #000040;">++</span><span style="color: #008080;">;</span>
    		<span style="color: #008000;">&#125;</span>
    	<span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">bool</span> pointer_dec_ref<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">void</span> <span style="color: #000040;">*</span>ptr <span style="color: #008000;">&#41;</span>
    <span style="color: #008000;">&#123;</span>
    	<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> ptr <span style="color: #000040;">!</span><span style="color: #000080;">=</span> <span style="color: #0000dd;">0</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    		pointer_map<span style="color: #008000;">&#91;</span>ptr<span style="color: #008000;">&#93;</span> <span style="color: #000040;">--</span><span style="color: #008080;">;</span>
    		<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> pointer_map<span style="color: #008000;">&#91;</span>ptr<span style="color: #008000;">&#93;</span> <span style="color: #000080;">==</span> <span style="color: #0000dd;">0</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    			pointer_map.<span style="color: #007788;">erase</span><span style="color: #008000;">&#40;</span>ptr<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    			<span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #008080;">;</span>
    		<span style="color: #008000;">&#125;</span>
    	<span style="color: #008000;">&#125;</span>
    	<span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #666666;">//&lt;/void&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">// ESTO VA EN LA CABECERA
    
    void pointer_inc_ref( void *ptr );
    bool pointer_dec_ref( void *ptr );
    	
    /**
     * Creates a smart pointer type that can free the memory used
     * automatically when it isn't necesary.
     * This pointer type can be very slow.
     */
    template&lt;typename _t&gt; class pointer_to {
    	Type *ptr;
    	
    public:
    	pointer_to( _t *pointer ) {
    		ptr = pointer;
    		pointer_inc_ref(ptr);
    	}
    		
    	pointer_to( const pointer_to&lt;_t&gt;&amp; pointer ) {
    		ptr = pointer.ptr;
    		pointer_inc_ref(ptr);
    	}
    		
    	template&lt;typename _u&gt; pointer_to( const pointer_to&lt;_u&gt;&amp; pointer ) {
    		ptr = dynamic_cast&lt;_t *&gt;( pointer.get() );
    		pointer_inc_ref( ptr );
    	}
    		
    	~pointer_to() {
    		if( pointer_dec_ref( ptr ) )
    			delete ptr;
    	}
    		
    	_t* get() const {
    		return ptr;
    	}
    		
    	_t* operator-&gt;() const {
    		return ptr;
    	}
    		
    	_t&amp; operator*() const {
    		return *ptr;
    	}
    
    	// &lt;/_t&gt;
    	pointer_to&lt;_t&gt;&amp; // &lt;/_t&gt;
    	operator=( const pointer_to&lt;_t&gt;&amp; pointer ) {
    		// &lt;/_t&gt;
    		if( pointer_dec_ref(ptr) )
    			delete ptr;
    		ptr = pointer.ptr;
    		pointer_inc_ref(ptr);
    	}
    		
    	pointer_to&lt;_t&gt;&amp; operator=( _t*pointer ) {
    		if( pointer_dec_ref(ptr) )
    			delete ptr;
    		ptr = pointer;
    		pointer_inc_ref(ptr);
    		return *this;
    	}
    		
    	template&lt;typename _u&gt; pointer_to&lt;_t&gt;&amp; operator=( const pointer_to&lt;_u&gt;&amp; pointer ) {
    		if( pointer_dec_ref(ptr) )
    			delete ptr;
    		ptr = dynamic_cast&lt;_t&gt;( pointer.ptr );
    		pointer_inc_ref(ptr);
    		return *this;
    	}
    }; // class pointer_to
    // &lt;/_t&gt;&lt;/_u&gt;&lt;/_t&gt;&lt;/typename&gt;&lt;/_t&gt;&lt;/_u&gt;&lt;/typename&gt;&lt;/_t&gt;&lt;/typename&gt;
    
    
    // ESTO VA EN EL CODIGO
    
    typedef map&lt;void *, int&gt; pointer_map_t;
    typedef pointer_map_t::iterator pointer_map_iterator;
    //&lt;/void&gt;
    static map&lt;void *, int&gt; pointer_map;
    
    void pointer_inc_ref( void *ptr )
    {
    	if( ptr != 0 ) {
    		pointer_map_iterator it;
    		it = pointer_map.find( ptr );
    		if( it == pointer_map.end() ) {
    			pointer_map.insert(pointer_map_t::value_type(ptr, 1));
    		}
    		else {
    			pointer_map[ptr] ++;
    		}
    	}
    }
    
    bool pointer_dec_ref( void *ptr )
    {
    	if( ptr != 0 ) {
    		pointer_map[ptr] --;
    		if( pointer_map[ptr] == 0 ) {
    			pointer_map.erase(ptr);
    			return true;
    		}
    	}
    	return false;
    }
    //&lt;/void&gt;</p></div>
    ";}
categories:
  - Desarrollo

---
En el artículo anterior nos quedamos con que hacía falta añadir nuevas funcionalidades que nos permitan mejorar las características del invento. Así que vamos a empezar poco a poco.

Para empezar, vamos a suponer que queremos poder asignar un puntero con el operador =. Para ellos hacemos lo siguiente:

<pre lang="cpp" line="1">template&lt;typename _t> class PtrSimple2 {
[..]
   PtrSimple2&lt;_t>&
   // &lt;/_t>
   operator=( const PtrSimple2&lt;_t>& ptr ) {
      // Hay que decrementar el puntero viejo, y en caso necesario
      // liberar la memoria
      (*_count) = (*_count) - 1;
      if( *_count == 0 ) {
         delete _count;
         delete _ptr;
      }
      _count = ptr._count;
      _ptr = ptr._ptr;
      (*_count) = (*_count) + 1;

      return *this;
   }
[..]
};
//&lt;/_t>&lt;/typename>
</pre>

Con esto ya tendríamos la asignación, pero sigue existiendo un problema de base: ¿qué pasa con la herencia? Por ejemplo, tenemos una clase A y otra B que hereda de A. Si yo creo que puntero de tipo A y otro de tipo B, me gustaría poder pasar sin problemas de uno a otro y que lo reconozca (¿sería lo lógico, no?). Pues tal y como están las cosas ahora, no lo haría (haced la prueba si no me creéis). Para solventar esto, añadimos los siguientes fragmentos de código:

<pre lang="cpp" line="1">template&lt;typename _t> class PtrSimple2 {
//&lt;/typename>
[..]
public:
   // Para poder leer el puntero sin problemas
   _t* get_ptr() {
      return _ptr;
   }

   // Nuevo constructor
   // Estoy simplificando algunas cosas, es posible que no se pueda acceder
   // directamente a los miembros del otro puntero
   template&lt;typename _u> PtrSimple2( const PtrSimple2&lt;_u>& ptr ) {
      _count = ptr._count;
      _ptr = dynamic_cast&lt;_t *>( ptr._ptr );
      (*count) = (*count) + 1;
   } // &lt;/_t>&lt;/_u>&lt;/typename>

   // Con el operador = hay que hacer lo mismo
   template&lt;typename _u> PtrSimple2&lt;_t>& operator=( const PtrSimple2&lt;_u>& ptr ) {
      // Hay que decrementar el puntero viejo, y en caso necesario
      // liberar la memoria
      (*_count) = (*_count) - 1;
      if( *_count == 0 ) {
         delete _count;
         delete _ptr;
      }
      _count = ptr._count;
      _ptr = dynamic_cast&lt;_t *>( ptr._ptr );
      (*_count) = (*_count) + 1;

      return *this;
   }
[..]
};
//&lt;/_t>&lt;/_u>&lt;/_t>&lt;/typename>
</pre>

¿Con esto ya estaría todo resuelto, no? Podemos controlar la herencia, los punteros, etc. Eso sí, siempre y para todo hay que utilizar este tipo de dato. Entonces, ¿puede haber casos en los que esto no funcione? La respuesta es sí. Imaginemos que tenemos que pasar a un método el la dirección a la que apuntamos (lo que hacemos con _get_ptr_) y luego podemos, desde otro lado, tomar dicha dirección en otro puntero.

Esta situación tan incomoda se pude solucionar con una política aún más agresiva de control de punteros. Para esto, debemos separar la parte de los contadores de punteros de la del propio control de los punteros. Vamos a ver otra clase para hacer punteros inteligentes que sigue una política un poco más agresiva:

<pre lang="cpp" line="1">// ESTO VA EN LA CABECERA

void pointer_inc_ref( void *ptr );
bool pointer_dec_ref( void *ptr );
	
/**
 * Creates a smart pointer type that can free the memory used
 * automatically when it isn't necesary.
 * This pointer type can be very slow.
 */
template&lt;typename _t> class pointer_to {
	Type *ptr;
	
public:
	pointer_to( _t *pointer ) {
		ptr = pointer;
		pointer_inc_ref(ptr);
	}
		
	pointer_to( const pointer_to&lt;_t>& pointer ) {
		ptr = pointer.ptr;
		pointer_inc_ref(ptr);
	}
		
	template&lt;typename _u> pointer_to( const pointer_to&lt;_u>& pointer ) {
		ptr = dynamic_cast&lt;_t *>( pointer.get() );
		pointer_inc_ref( ptr );
	}
		
	~pointer_to() {
		if( pointer_dec_ref( ptr ) )
			delete ptr;
	}
		
	_t* get() const {
		return ptr;
	}
		
	_t* operator->() const {
		return ptr;
	}
		
	_t& operator*() const {
		return *ptr;
	}

	// &lt;/_t>
	pointer_to&lt;_t>& // &lt;/_t>
	operator=( const pointer_to&lt;_t>& pointer ) {
		// &lt;/_t>
		if( pointer_dec_ref(ptr) )
			delete ptr;
		ptr = pointer.ptr;
		pointer_inc_ref(ptr);
	}
		
	pointer_to&lt;_t>& operator=( _t*pointer ) {
		if( pointer_dec_ref(ptr) )
			delete ptr;
		ptr = pointer;
		pointer_inc_ref(ptr);
		return *this;
	}
		
	template&lt;typename _u> pointer_to&lt;_t>& operator=( const pointer_to&lt;_u>& pointer ) {
		if( pointer_dec_ref(ptr) )
			delete ptr;
		ptr = dynamic_cast&lt;_t>( pointer.ptr );
		pointer_inc_ref(ptr);
		return *this;
	}
}; // class pointer_to
// &lt;/_t>&lt;/_u>&lt;/_t>&lt;/typename>&lt;/_t>&lt;/_u>&lt;/typename>&lt;/_t>&lt;/typename>


// ESTO VA EN EL CODIGO

typedef map&lt;void *, int> pointer_map_t;
typedef pointer_map_t::iterator pointer_map_iterator;
//&lt;/void>
static map&lt;void *, int> pointer_map;

void pointer_inc_ref( void *ptr )
{
	if( ptr != 0 ) {
		pointer_map_iterator it;
		it = pointer_map.find( ptr );
		if( it == pointer_map.end() ) {
			pointer_map.insert(pointer_map_t::value_type(ptr, 1));
		}
		else {
			pointer_map[ptr] ++;
		}
	}
}

bool pointer_dec_ref( void *ptr )
{
	if( ptr != 0 ) {
		pointer_map[ptr] --;
		if( pointer_map[ptr] == 0 ) {
			pointer_map.erase(ptr);
			return true;
		}
	}
	return false;
}
//&lt;/void>
</pre>

En este caso, estamos haciendo una política muy agresiva, pero ya se controlan casi todos los casos (aún pueden existir problemas, para los que la política a utilizar sería que el puntero inteligente no libere la memoria [por lo que sería una perdida utilizarlo]). Además, existen problemas de dobles enlaces que podrían provocar que la memoria nunca se libere.

Seguro que hay mejores modos de hacerlo, pero este es, el que a partir de algunas cosillas que he leído por ahí he conseguido implementar. Si hay alguna pregunta (y habéis sido capaces de leer hasta aquí) no os cortéis en hacerla.