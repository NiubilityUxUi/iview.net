<template>
    <div :class="wrapClasses" :style="styles">
        <div :class="classes">
            <div :class="[prefixCls + '-header']" v-if="showHeader" ref="header" @mousewheel="handleMouseWheel">
                <data-grid-head
                    :prefix-cls="prefixCls"
                    :columns="cloneColumns"></data-grid-head>
            </div>
        </div>
    </div>
</template>
<script>
    import dataGridHead from './data-grid-head.vue';
    import dataGridBody from './data-grid-body.vue';

    import { oneOf, getStyle, deepCopy, getScrollBarSize } from '../../utils/assist';
    import { on, off } from '../../utils/dom';

    const prefixCls = 'ivu-table';

    let rowKey = 1;
    let columnKey = 1;

    export default {
        name: 'DataGrid',
        mixins: [ Locale ],
        components: { dataGridHead, dataGridBody },
        props: {
            columns:{
                type: Array,
                default:[]
            },
            dataSource:{
                type: Object,
                default:{}
            },
        },
        data () {
            return {
                ready: false,
                tableWidth: 0,
                columnsWidth: {},
                prefixCls: prefixCls,
                compiledUids: [],
                objData: this.makeObjData(),     // checkbox or highlight-row
                rebuildData: [],    // for sort or filter
                cloneColumns: this.makeColumns(),
                showSlotHeader: true,
                showSlotFooter: true,
                bodyHeight: 0,
                bodyRealHeight: 0,
                scrollBarWidth: getScrollBarSize(),
                currentContext: this.context,
                cloneData: deepCopy(this.data)
            };
        },
        computed: {
            
        },
        methods: {
            
        }
    };
</script>
