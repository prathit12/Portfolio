<template>
    <div>
        <div class="photo">
            <a>
                <img :src="getImageURL('user.photo')" alt="photo"/>
            </a>

        </div>
    </div>
</template>

<script>
    export default{
        name:'photo',
        props:['user'],
        methods: {
            getImageURL(img){
                return require('../assets/img/'+img);
            },
        },
    };
</script>

<style scoped lang="scss">
    .photo {
        a:focus {
            outline: none;
        }
        img {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            display: inline-block;
        }
    }
    img {
        max-width: 100%;
    }
</style>