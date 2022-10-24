## Table of Contents

https://uab-it.github.io/linear/components/table-of-contents.html#usage

https://libraries.io/bower/jquery-toc/v0.0.1

```html
<script>
  jQuery(document).ready( function() {
    var TOCcontainer = document.querySelector(‘#toc’);
    var toc = initTOC({
      selector: ‘h3, h4, h5’,
      scope: ‘#content’,
      overwrite: false,
      prefix: ‘toc’
    });
    TOCcontainer.appendChild(toc);
  });
</script>
```

```html
<nav id="toc" class="table-of-contents">
  <p><strong>Contents</strong></p>
</nav>
```

Translate Jquery

https://github.com/nefe/You-Dont-Need-jQuery#query-selector

//Document Ready

```
if (document.readyState !== 'loading') {
    eventHandler();
  } else {
    document.addEventListener('DOMContentLoaded', eventHandler);
  }
```

// Assign variable for id

```
document.querySelector('#id');
```

// toc headers

```
var toc = initTOC(options);
initTOC({
    selector: 'h1, h2, h3, h4, h5, h6',
    scope: 'body',
    overwrite: false,
    prefix: 'toc'
});
```

Final

```
if (document.readyState !== 'loading') {
  eventHandler(){
  var container = document.querySelector('#toc');
  var toc = initTOC({
    selector: 'h3, h4, h5',
    scope: '#content',
    overwrite: false,
    prefix: 'toc'
  });

  container.appendChild(toc);
  }
} else {
  document.addEventListener('DOMContentLoaded', eventHandler);
}


```
