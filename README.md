# JavaScript_learning

## First_day

### Syntactic sugar
语法糖: CoffeeScript

### Handbook
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference

### Compatibility
http://caniuse.com 

### Type attribute for JS
<script type=""></script>
Nolonger in ues
Also for language attributes
<script language=""></script>

### If include src attribute, inner code is invalid
Like: 
<script src="file.js">
  alert(1); // 此内容会被忽略，因为设定了 src
</script>
Must write like:
<script src="file.js"></script>
<script>
  alert(1);
</script>