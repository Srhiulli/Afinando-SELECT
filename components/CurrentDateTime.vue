<script setup>
import dayjs from 'dayjs'

const currentDate = dayjs().format('HH[hrs] DD-MM')

</script>

<template>
  <div>
    <p> {{ currentDate }}</p>
  </div>
</template>