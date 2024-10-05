<template>
    <main>
        <section id="home">
            <div class="container">
                <div class="content">
                    <div class="text_description">
                        <h3>SO, YOU WANT TO TRAVEL TO</h3>
                        <h1>SPACE</h1>
                        <P>Let’s face it; if you want to go to space, you might as well genuinely go to
                            outer space and not hover kind of on the edge of it. Well sit back, and relax
                            because we’ll give you a truly out of this world experience!</P>
                    </div>
                    <RouterLink to="/destination" class="explore">EXPLORE</RouterLink>
                    <!-- <div class="explore">EXPLORE</div> -->
                </div>
            </div>
        </section>
    </main>
</template>


<script setup lang="ts">

</script>


<style scoped>
main {
    color: #fff;
}

#home {
    width: 100%;
    background-image: url(/src/assets/home/background-home-desktop.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    padding: 0;
    margin: 0;
}

.container {
    max-width: 1044px;
    margin: 0 auto;
}

.content {
    width: 100%;
    display: flex;
    min-height: calc(100vh - 92px);
    justify-content: space-between;
    align-items: center;
    padding-top: 92px;
}

.text_description {
    width: 380px;
    padding: 10px 0;
    display: flex;
    flex-direction: column;
}

p {
    line-height: 25px;
    color: #ffffffcc;
}

h3 {
    color: #ffffffcc;
    font-weight: 5;
    letter-spacing: 5px;
    font-size: 16px;
}

h1 {
    font-size: 90px;
    font-weight: 5;
    letter-spacing: 10px;
    margin: 0;
}

.explore {
    width: 150px;
    height: 150px;
    background-color: #fff;
    color: #000;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 80px;
}

@media screen and (max-width: 1024px) {
    body {
        width: 100%;
    }

    .header {
        width: 100%;
    }

    .container {
        max-width: 80%;
    }
}

@media screen and (max-width: 768px) {
    body {
        width: 100%;
    }

    .header {
        width: 100%;
    }

    .container {
        max-width: 80%;
    }

    .content {
        width: 100%;
        display: flex;
        flex-direction: column;
        gap: 150px;
        padding: 92px 0;
    }

    #home {
        background: url(/src/assets/home/background-home-tablet.jpg);
        background-size: cover;
        min-width: 100%;
        background-repeat: no-repeat;
        /* height: 100%; */
    }

    .text_description {
        text-align: center;
        width: 100%;
    }

    h1 {
        font-size: 150px;
    }
}

@media screen and (max-width: 375px) {
    main {
        width: 100%;
    }

    #home {
        background: url(/src/assets/home/background-home-mobile.jpg);
        background-size: cover;
        min-width: 100%;
        background-repeat: no-repeat;
        /* height: 100%; */
    }

    h1 {
        font-size: 30px;
    }
    .container{
        max-width: 80%;
        margin: 0 auto;
    }
    .content {
        gap: 50px;
    }
}
</style>
