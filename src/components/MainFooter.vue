<template>
    <footer>
        <div class="down">
            <h3>さあ行こう</h3>
            <h4>Lets Go</h4>
            <h5>&copy; 2023</h5>
        </div>
    </footer>
</template>

<script>
export default {
    name: 'MainFooter'
}
</script>

<style scoped>
footer {
    background: black;
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 15px;
}
.down {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    text-align: center;
    color: #fff;
}
</style>