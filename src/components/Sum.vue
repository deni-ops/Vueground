<template>

  <div>
    First to sum (const): {{sum1}} <br>
    Second to sum (const): {{sum2}} <br>
    Sum of previous two numbers: {{ res }} <br>
  </div>

</template>


<script>

export default {
  name: 'Sum',
  props: {
    sum1: {
      type: Number,
    },

    sum2: {
      type: Number,
    }
  },
  computed: {
    res: function() {
      return this.sum1+this.sum2
    }
  },
}

</script>
