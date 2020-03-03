<template>
  <div class="well">
    <h3>History</h3>
    <ul class="list-group text-left">
      <li class="list-group-item" v-for="item in history">
        <div> 
          <strong>{{ item.fromLang}} => {{item.toLang}}</strong>
        </div>
        <br />
        <div>
          <strong class="text-success">{{ item.fromText }} :</strong>
          <span class="text-info">{{ item.toText }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["history"],
  data() {
    return {};
  }
};
</script>

<style>
</style>