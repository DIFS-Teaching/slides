# Schéma třívrstvé architektury
<!-- .slide: class="normal centered fullspace" data-transition="slide-in fade-out" -->

![Třívrstvá architektura](assets/3tier1.svg) <!-- .element: style="height:750px;margin:0;" -->

<div class="fragment box shadow" style="position:absolute;left:1200px;top:840px;padding:10px;">
Database server<br/>
(MySQL, Oracle, ...)
</div>

<div class="fragment box shadow" style="position:absolute;left:1200px;top:240px;padding:10px;">
Web browser
</div>

<div class="fragment box shadow" style="position:absolute;left:1200px;top:540px;padding:10px;">
Application server<br/>
(Java, .NET, ...)
</div>

<div class="fragment box shadow" style="position:absolute;right:1200px;top:320px;padding:10px;">
HTTP<br/>
(přenos dat, serializace)
</div>

<div class="fragment box shadow" style="position:absolute;right:1200px;top:780px;padding:10px;">
SQL<br/>
</div>

---

# Schéma třívrstvé architektury (II)
<!-- .slide: class="normal centered fullspace" data-transition="fade-in slide-out" -->

![Třívrstvá architektura](assets/3tier2.svg) <!-- .element: style="height:750px;margin:0;" -->

<div class="fragment box shadow" style="position:absolute;left:1200px;top:540px;padding:10px;">
Java, .NET, PHP ...<br/>
Různá rámcová řešení (framework)
</div>

<div class="fragment box shadow" style="position:absolute;left:1200px;top:240px;padding:10px;">
Tenčí nebo tlustší klient v prohlížeči
</div>

<div class="fragment box shadow" style="position:absolute;left:1200px;top:840px;padding:10px;">
Datový model (objektový, relační, ...)
</div>

---

# Webový IS

<!-- .slide: class="normal centered fullspace" -->
![Graf funkce](assets/backend1.svg) <!-- .element: style="height:800px;margin:0;" -->


---

# Webový IS s aplikačním rozhraním

<!-- .slide: class="normal centered fullspace" -->
![Graf funkce](assets/backend2.svg) <!-- .element: style="height:800px;margin:0;" -->
