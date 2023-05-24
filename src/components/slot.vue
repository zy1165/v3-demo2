<template>
    <div>
        <main>
            <slot></slot>
        </main>
        <header>
            <slot name="header"></slot>
        </header>
        <section>
            <slot name="section"></slot>
        </section>
        <footer>
            <slot name="footer" :cotxt="str"></slot>
        </footer>
    </div>
</template>

<script setup>
let str = '我们来组成腿部🤼‍♀️'

</script>

<style lang="scss" scoped></style>