<template>
  <div>
    <h1 class="contato" v-show="open">telefone: (11) 99999-9999 | email: 5vXZt@example.com</h1>
  </div>
</template>

<script>
export default {
  name: "contato",
  props: ["open"],
};
</script>