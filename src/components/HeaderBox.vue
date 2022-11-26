<template>
    <div>
        <ul class="nav">
  <li class="nav-item">
    <a class="nav-link disable" aria-current="page" href="#"><b>Fancy Quiz App</b></a>
  </li>
  <li class="nav-item">
    <a class="nav-link" href="#">Counter: {{ numCorrect }}/{{ numTotal }}</a>
  </li>
</ul>
    </div>
</template>

<script>
export default {
  props:[
    'numCorrect',
    'numTotal'
  ]
}
</script>