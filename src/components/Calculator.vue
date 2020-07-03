<template>
    <div class="calculator"> 
        <div>hello</div>
        <div>hello</div>
        <div>hello</div>
        <div>hello</div>
        <div>hello</div>
        <div>hello</div>
    </div>
</template>

<script> 
export default{
}
</script> 

<style scooped> 
.calculator {
    display:grid;  
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px, auto);
}
</style>