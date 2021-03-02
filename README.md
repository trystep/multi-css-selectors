# Поиск элементов с помощью составных CSS-селекторов

<article id="ember3982" class="step-show ember-view"><div class="step-dynamic-container">
<!---->
      <div id="ember3983" class="step-view step-view_material ember-view"><!----><div class="step-wrapper">
  <div class="step-inner page-fragment">
    <div id="ember3984" class="html-content rich-text-viewer ember-view" data-ready=""><span>

<p>Предположим, что не можем найти элемент на странице, используя простой&nbsp;селектор, так как такой селектор находит сразу несколько элементов. Ниже мы привели часть кода простой HTML-страницы, описывающей блог. Саму страницу&nbsp;вы можете посмотреть по <a href="http://suninjuly.github.io/blog_example.html" rel="noopener noreferrer nofollow" target="_blank">ссылке</a>.</p>

<p>Вопрос: как нам найти селектор для подписи у второй картинки? Вот здесь нам поможет иерархическая структура страницы и возможность комбинировать&nbsp;CSS-селекторы. CSS-селекторы позволяют использовать одновременно любые селекторы, рассмотренные ранее, а также имеют некоторые дополнительные возможности для уточнения поиска.</p>

<pre><code class="language-html hljs xml"><span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">id</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"posts"</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">class</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"post-list"</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">id</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"post1"</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">class</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"item"</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; &nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">class</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"title"</span></span></span><span class="hljs-tag">&gt;</span></span>Как я провел лето<span class="hljs-tag"><span class="hljs-tag">&lt;/</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; &nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">img</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">src</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"./images/summer.png"</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;/</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">id</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"post2"</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">class</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"item"</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; &nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">class</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"title second"</span></span></span><span class="hljs-tag">&gt;</span></span>Ходили купаться<span class="hljs-tag"><span class="hljs-tag">&lt;/</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; &nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">img</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">src</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"./images/bad_dog.jpg"</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;/</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">id</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"post3"</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">class</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"item"</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; &nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">class</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"title"</span></span></span><span class="hljs-tag">&gt;</span></span>С друзьями<span class="hljs-tag"><span class="hljs-tag">&lt;/</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; &nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">img</span></span></span><span class="hljs-tag"> </span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">src</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"./images/friends.jpg"</span></span></span><span class="hljs-tag">&gt;</span></span>
&nbsp; <span class="hljs-tag"><span class="hljs-tag">&lt;/</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag">&gt;</span></span>
<span class="hljs-tag"><span class="hljs-tag">&lt;/</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">div</span></span></span><span class="hljs-tag">&gt;</span></span>
</code></pre>

<p><strong>Использование потомков</strong></p>

<p>Попробуем найти элемент с текстом "Ходили купаться". Для решения этой задачи мы можем взять элемент, стоящий выше в иерархии нужного нам элемента,&nbsp;и написать следующий селектор:</p>

<p><strong>"#post</strong><strong>2 .title"</strong></p>

<p>Здесь знак <strong>"#"</strong> означает, что надо искать элемент с&nbsp;id "post2", а <strong>"."</strong>&nbsp;— что искать надо класс со значением "title".</p>

<p>Элемент ".title" называется&nbsp;<strong>потомком</strong> (англ.&nbsp;<strong>descendant</strong>) элемента "#post2". Потомок может находиться на любом уровне вложенности&nbsp;— все элементы&nbsp;с селектором ".title"&nbsp;также являются и потомками элемента "#posts", хотя и расположены от него на два уровня ниже. <strong>"#posts .title" </strong>найдет все 3 элемента с классом "title".</p>

<p><span style="color: #ff4363;">!Внимание.</span> Символ пробела " " является значащим в CSS-селекторах.&nbsp;Это важный символ, который разделяет описание предка и потомка. Если бы мы записали селектор "<strong>#post</strong><strong>2.title"&nbsp;</strong>без пробела, то в данном примере не было найдено ни одного элемента. Такая запись означала бы, что мы хотим найти элемент, который одновременно содержит&nbsp;id "post2" и класс "title".&nbsp;То есть&nbsp;<strong>"#post2 .title" </strong>и&nbsp;<strong>"#post2.title"&nbsp;</strong>— это&nbsp;разные селекторы<strong>.</strong></p>

<p><strong>Использование дочерних элементов</strong></p>

<p>Другой способ найти этот элемент:</p>

<p><strong>"#post2 &gt; div.title"</strong></p>

<p>Здесь мы указали еще тег элемента&nbsp;<strong>div&nbsp;</strong>и уточнили, что нужно взять элемент с тегом и классом:&nbsp;<strong>"div.title"</strong>, который находится строго на один уровень иерархии ниже чем элемент&nbsp;<strong>"#post2"</strong>&nbsp;(это задаёт символ&nbsp;"&gt;").</p>

<p>Элемент "#post2" в этом случае называется <strong>родителем</strong> (англ. <strong>parent</strong>) для элемента<strong> "div.title"</strong>, а элемент <strong>"div.title"</strong> называется <strong>дочерним элементом</strong> (англ. <strong>child</strong>) для элемента <strong>"#post2"</strong>. Если символа&nbsp;<strong>"&gt;"</strong> нет, то будет выполнен поиск&nbsp;всех элементов&nbsp;<strong>"div.title"</strong> на любом уровне ниже первого элемента.</p>

<p><span style="color: #ff4363;">!Внимание.&nbsp;</span>В данном случае символы пробела вокруг символа "&gt;"&nbsp;не несут важного значения&nbsp;в отличие от предыдущего примера,&nbsp;и могут быть опущены. Запись&nbsp;<strong>"#post2&gt;div.title"&nbsp;</strong>аналогична записи&nbsp;<strong>"#post2 &gt; div.title"</strong>.</p>

<p><strong>Использование порядкового номера дочернего элемента</strong></p>

<p>Еще один способ найти этот элемент:</p>

<p><strong>"#posts &gt; .item:nth-child(2) &gt; .title"</strong></p>

<p>Псевдо-класс&nbsp;<strong>:nth-child(2)</strong>&nbsp;— позволяет найти&nbsp;второй по порядку&nbsp;элемент&nbsp;среди дочерних элементов для "#posts<strong>"</strong>. Затем с помощью "&gt; .title" мы указываем, что нам нужен элемент ".title", родителем которого является найденный ранее элемент ".item".</p>

<p><strong>Использование нескольких классов</strong></p>

<p>Также мы можем использовать сразу несколько классов элемента, чтобы его найти. Для этого классы записываются подряд через точку: <strong>".title.second"</strong></p>

<p>Мы рассмотрели базовые селекторы, которых будет достаточно для написания простых UI-тестов. Если вы захотите разобраться подробнее в css-селекторах, то мы рекомендую вам посмотреть следующие статьи:&nbsp;</p>

<p><a href="https://learn.javascript.ru/css-selectors" rel="nofollow noopener noreferrer" target="_blank">https://learn.javascript.ru/css-selectors</a></p>

<p><a href="https://www.w3schools.com/cssref/css_selectors.asp" rel="nofollow noopener noreferrer" target="_blank">https://www.w3schools.com/cssref/css_selectors.asp</a></p>

<p><a href="https://developer.mozilla.org/ru/docs/Web/CSS/CSS_%D0%A1%D0%B5%D0%BB%D0%B5%D0%BA%D1%82%D0%BE%D1%80%D1%8B" rel="nofollow noopener noreferrer" target="_blank">https://developer.mozilla.org/ru/docs/Web/CSS/CSS_%D0%A1%D0%B5%D0%BB%D0%B5%D0%BA%D1%82%D0%BE%D1%80%D...</a></p></span></div>
    </div>
</div>
</div>
</div>
</article>
