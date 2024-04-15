<script>
export default {
    props: {
        columns: {
            type: Array,
            default: () => []
        }
    },
    data() {
        return {}
    },
    computed: {
        handle(val) {
            let arr = Object.keys(val._events)
            let obj = {}
            arr.forEach(item => {
                obj[item] = val._events[item][0].fns
            })
            return obj
        }
    },
}
</script>

<template>
    <el-table style="width: 100%" v-bind="$attrs" v-on="handle">
        <template v-for="(column,index) in columns">
            <!--如果column里面有slotName属性，就将slotName属性的值作为插槽的名字-->
            <el-table-column v-bind="column" v-if="column.slotName" :key="column.key || column.prop || index">
                <template v-if="column.slotName" slot-scope="scope">
                    <slot :name="column.slotName" v-bind="scope"></slot>
                </template>
            </el-table-column>
            <el-table-column v-else v-bind="column"></el-table-column>
        </template>
    </el-table>
</template>

<style scoped lang="scss">

</style>