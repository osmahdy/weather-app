<template>
    <div class="center">
        <div class="details">
            <div class="left">
                <div class="degree">
                    <p>{{ temp }}</p>
                    <span>o</span>
                </div>
                <p>{{ status }}</p>
            </div>
            <div class="right">
                <div>
                    <i class="fa-solid fa-wind"></i>
                    <p>{{ wind }}</p>
                </div>
                <div>
                    <i class="fa-solid fa-droplet"></i>
                    <p>{{ hum + '%'}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'mainWedgit',
    props: ['temp','wind','hum','status'],
}
</script>


<style>
.center {
    margin: 20px 0;
    width: 100%;
}
.center .details{
    display: flex;
    justify-content: center;
    margin: 50px auto;
    padding: 20px;
}
.center .details p {
    font-weight: 500;
}
.center .details .left {
    position: relative;
    padding: 20px;
}
.center .details .left .degree  {
    display: flex;
}
.center .details .left .degree p{
    font-size: 120px;
    font-weight: bold;
}
.center .details .left .degree span{
    font-size: 50px;
    font-weight: bold;
}
.center .details .right {
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.center .details .right > div {
    display: flex;
    margin: 10px 0;
    width: 100%;
    font-size: 14px;
}
.center .details .right > div i {
    font-size: 18px;
}
.center .details .right > div p {
    margin-left: 10px;
}
@media (max-width: 990px){
    .center .details {
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
}
</style>