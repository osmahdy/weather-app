<template>
      <!-- <div class="bottom"> -->
        <div class="card">
            <p>{{ day }}</p>
            <div class="degree">
                    <p>{{ temp }}</p>
                    <span>o</span>
            </div>
            <p>{{ status }}</p>
        </div>
    <!-- </div> -->
</template>

<script>
export default {
    name: 'cardsComp',
    props: ['day','temp','status']
}
</script>

<style scoped>

  .card {
    border: 2px solid #eee;
    padding: 5px;
    margin: 10px;
    border-radius: 20px;
    cursor: pointer;
    transform: scale(1);
    transition: .3s;
}
  .card p {
    font-size: 13px;
    margin: 10px 0;
}
  .card p:first-child {
    font-weight: 600;
}
  .card .degree {
    display: flex;
    justify-content: center;
}
  .card .degree p {
    font-size: 16px;
    font-weight: 500;
}
  .card .degree span {
    font-size: 14px;
}
</style>