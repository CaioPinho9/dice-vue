<template>
    <footer id="footer">
        <div>
            <p>Dice Forge 2022</p>
            <a href="https://github.com/CaioPinho9">Github: CaioPinho9</a>
            
        </div>
    </footer>
</template>

<script>
export default {
    name: 'Footer'
}
</script>

<style scoped>
    #footer {
        height: 70px;
        background-color: #222;
        border-top: 4px solid #ff8800 ;
        color: #ff8800 ;
        display: flex;
        align-items: center;
        justify-content: center;
        bottom: 0;
        width: 100%;
        text-align: center;
    }

    a {
        color: #ff8800 ;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }

    a:hover {
        color: #FFF;
    }

</style>