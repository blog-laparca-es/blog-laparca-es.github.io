---
title: A vueltas con las plantillas
author: laparca
type: post
date: 2009-05-29T08:58:40+00:00
url: /2009/05/29/a-vueltas-con-las-plantillas/
openid_comments:
  - 'a:2:{i:0;s:5:"47161";i:1;s:5:"47163";}'
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:4062:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> T, <span style="color: #0000ff;">typename</span> Proxy <span style="color: #000080;">=</span> queue_proxy<span style="color: #000080;">&lt;</span>T<span style="color: #000080;">&gt;</span> <span style="color: #000080;">&gt;</span>
    <span style="color: #0000ff;">class</span> channel
    <span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">public</span><span style="color: #008080;">:</span>
    	<span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> Result<span style="color: #000080;">&gt;</span>
    	channel<span style="color: #000080;">&lt;</span>Result, <span style="color: #0000ff;">typename</span> Proxy<span style="color: #008080;">::</span><span style="color: #0000ff;">template</span> bind<span style="color: #000080;">&lt;</span>Result<span style="color: #000080;">&gt;</span><span style="color: #008080;">::</span><span style="color: #007788;">type</span><span style="color: #000080;">&gt;</span>
    	operator<span style="color: #000080;">&gt;&gt;</span><span style="color: #008000;">&#40;</span>Result <span style="color: #008000;">&#40;</span><span style="color: #000040;">&amp;</span>receiver<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#40;</span>T<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span>
    	<span style="color: #008000;">&#123;</span>
    		channel<span style="color: #000080;">&lt;</span>Result, <span style="color: #0000ff;">typename</span> Proxy<span style="color: #008080;">::</span><span style="color: #0000ff;">template</span> bind<span style="color: #000080;">&lt;</span>Result<span style="color: #000080;">&gt;</span><span style="color: #008080;">::</span><span style="color: #007788;">type</span><span style="color: #000080;">&gt;</span> out_channel<span style="color: #008080;">;</span>
    		threads.<span style="color: #007788;">push_back</span><span style="color: #008000;">&#40;</span><span style="color: #0000dd;">new</span> boost<span style="color: #008080;">::</span><span style="color: #007788;">thread</span><span style="color: #008000;">&#40;</span>create_stream_channel_thread<span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span><span style="color: #0000dd;">this</span>, out_channel, receiver<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    		<span style="color: #0000ff;">return</span> channel<span style="color: #000080;">&lt;</span>Result, <span style="color: #0000ff;">typename</span> Proxy<span style="color: #008080;">::</span><span style="color: #0000ff;">template</span> bind<span style="color: #000080;">&lt;</span>Result<span style="color: #000080;">&gt;</span><span style="color: #008080;">::</span><span style="color: #007788;">type</span><span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span>out_channel<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    	<span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">template&lt;typename T, typename Proxy = queue_proxy&lt;T&gt; &gt;
    class channel
    {
    public:
    	template&lt;typename Result&gt;
    	channel&lt;Result, typename Proxy::template bind&lt;Result&gt;::type&gt;
    	operator&gt;&gt;(Result (&amp;receiver)(T))
    	{
    		channel&lt;Result, typename Proxy::template bind&lt;Result&gt;::type&gt; out_channel;
    		threads.push_back(new boost::thread(create_stream_channel_thread(*this, out_channel, receiver)));
    		return channel&lt;Result, typename Proxy::template bind&lt;Result&gt;::type&gt;(out_channel);
    	}
    };</p></div>
    ";i:2;s:2579:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">int</span> fac<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> x<span style="color: #008000;">&#41;</span>
    <span style="color: #008000;">&#123;</span>
    	<span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span>x <span style="color: #000080;">&lt;</span> <span style="color: #0000dd;">1</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">return</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
    	<span style="color: #0000ff;">return</span> x <span style="color: #000040;">*</span> fac<span style="color: #008000;">&#40;</span>x<span style="color: #000040;">-</span><span style="color: #0000dd;">1</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> show<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> x<span style="color: #008000;">&#41;</span>
    <span style="color: #008000;">&#123;</span>
    	std<span style="color: #008080;">::</span><span style="color: #0000dd;">cout</span> <span style="color: #000080;">&lt;&lt;</span> x <span style="color: #000080;">&lt;&lt;</span> std<span style="color: #008080;">::</span><span style="color: #007788;">endl</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/* some code here */</span>
    &nbsp;
    channel<span style="color: #000080;">&lt;</span><span style="color: #0000ff;">int</span><span style="color: #000080;">&gt;</span> ch<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/* Se redirige el canal a fac y la salida del factorial a show */</span>
    ch <span style="color: #000080;">&gt;&gt;</span> fac <span style="color: #000080;">&gt;&gt;</span> show<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/* more code here */</span></pre></td></tr></table><p class="theCode" style="display:none;">int fac(int x)
    {
    	if(x &lt; 1) return 1;
    	return x * fac(x-1);
    }
    
    void show(int x)
    {
    	std::cout &lt;&lt; x &lt;&lt; std::endl;
    }
    
    /* some code here */
    
    channel&lt;int&gt; ch;
    
    /* Se redirige el canal a fac y la salida del factorial a show */
    ch &gt;&gt; fac &gt;&gt; show;
    
    /* more code here */</p></div>
    ";i:3;s:1782:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">class</span> functor
    <span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">public</span><span style="color: #008080;">:</span>
    	functor<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span><span style="color: #008000;">&#125;</span>
    &nbsp;
    	<span style="color: #0000ff;">int</span> operator<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> a<span style="color: #008000;">&#41;</span>
    	<span style="color: #008000;">&#123;</span>
    		<span style="color: #ff0000; font-style: italic;">/* do something interesting */</span>
    	<span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/* some code here */</span>
    &nbsp;
    channel<span style="color: #000080;">&lt;</span><span style="color: #0000ff;">int</span><span style="color: #000080;">&gt;</span> ch<span style="color: #008080;">;</span>
    ch <span style="color: #000080;">&gt;&gt;</span> functor<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #000080;">&gt;&gt;</span> show<span style="color: #008080;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">class functor
    {
    public:
    	functor() {}
    
    	int operator()(int a)
    	{
    		/* do something interesting */
    	}
    };
    
    /* some code here */
    
    channel&lt;int&gt; ch;
    ch &gt;&gt; functor() &gt;&gt; show;</p></div>
    ";}
categories:
  - Desarrollo
tags:
  - c++
  - cpp
  - functores
  - plantillas
  - programacion
  - templates

---
Ando haciendo pruebas últimamente con C++ y hay algo que ahora no soy capaz de hacer, que es que elija entre un método u otro dependiendo de si lo que se le pasa por parámetro es una función o un functor.

Concretamente tengo algo como esto:

<pre lang="cpp">template&lt;typename T, typename Proxy = queue_proxy&lt;T> >
class channel
{
public:
	template&lt;typename Result>
	channel&lt;Result, typename Proxy::template bind&lt;Result>::type>
	operator>>(Result (&receiver)(T))
	{
		channel&lt;Result, typename Proxy::template bind&lt;Result>::type> out_channel;
		threads.push_back(new boost::thread(create_stream_channel_thread(*this, out_channel, receiver)));
		return channel&lt;Result, typename Proxy::template bind&lt;Result>::type>(out_channel);
	}
};
</pre>

La idea es que este código permite hacer algo como lo siguiente:

<pre lang="cpp">int fac(int x)
{
	if(x &lt; 1) return 1;
	return x * fac(x-1);
}

void show(int x)
{
	std::cout &lt;&lt; x &lt;&lt; std::endl;
}

/* some code here */

channel&lt;int> ch;

/* Se redirige el canal a fac y la salida del factorial a show */
ch >> fac >> show;

/* more code here */
</pre>

Sí, el código se parece mucho a Axum de Microsoft, que la idea es crear algo parecido para C++.

El caso es que el operador funciona bien cuando se pasan funciones, pero no funciona si le paso un functor, como podría ser el caso siguiente:

<pre lang="cpp">class functor
{
public:
	functor() {}

	int operator()(int a)
	{
		/* do something interesting */
	}
};

/* some code here */

channel&lt;int> ch;
ch >> functor() >> show;
</pre>

La cosa es que no sé como hacer para detectar que se me pasa un functor y qué parametros son los que tiene, aunque aún tengo que hacer alguna prueba más antes de dar por imposible la tarea.