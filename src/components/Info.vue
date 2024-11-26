<script>
</script>

<template>
    <footer class="w-full">
        <div class="info container mx-auto flex flex-wrap justify-center bg-cover pt-10">
            <div class="map mb-5 rounded-l-md">
                <iframe
                    src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3640.8676070038923!2d120.67096857501495!3d24.141287178405673!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x34693d0cf25b4517%3A0xc6a3c93dc5084762!2z5p6X5LmL5Yqp57SA5b-16aSo!5e0!3m2!1szh-TW!2stw!4v1728008463834!5m2!1szh-TW!2stw"
                    width="300" height="300" style="border:0;" allowfullscreen="" loading="lazy"
                    referrerpolicy="no-referrer-when-downgrade"></iframe>
            </div>
            <div class="place bg-white/30 w-500 mb-5 backdrop-blur-sm p-8 flex flex-col justify-center rounded-r-md">
                <div class="logo w-[200px] h-[50px] bg-contain bg-no-repeat"></div>
                <div class="text text-start my-4 text-black">
                    <div>開館時間： 週二~週六．11:00~17:00 </div>
                    <div>週日、週一及國定假日休館</div>
                    <div>聯絡電話： (04)2218-3652</div>
                    <div>聯絡地址： 403 臺中市西區柳川西路二段158號、162號 </div>
                    <div>電子信箱： chihchu@gm.ntcu.edu.tw </div>
                    <div>粉絲專頁： <a href="https://www.facebook.com/LinChihChuMemorial/">林之助紀念館</a></div>
                </div>
            </div>
            <div class="w-full h-auto py-4 text-center font-bold">Copyright © 2024林之助紀念館 / 2024 Lin, Chih-Chu
                Memorial. All rights reserved.</div>
        </div>
    </footer>


</template>

<style scoped>
.info {
    background-image: url('../assets/img/bg_footer.png');
}

.logo {
    background-image: url('../assets/img/logo.png');
}
a {
  text-decoration: none;
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    border-radius: 5px;
    background-color: #8b6c6f;
  }
}

</style>