<template>
 <tr>
      <td>{{contact.index}}</td>
      <td>{{contact.name}}</td>
      <td>{{contact.phone}}</td>
    </tr>
</template>

<script>
export default {
  props: ["contacts"]
}
</script>