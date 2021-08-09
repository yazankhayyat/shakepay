<template>
    <el-table
        class="table-responsive table-flush"
        header-row-class-name="thead-light"
        :header-cell-class-name="headerCellClasses"
        :data="data"
        :empty-text="emptyText"
        :max-height="maxHeight"
        :row-class-name="styleRow"
        :show-summary="showSummary"
        :row-key="currentId"
        :sum-text="sumText"
        :summary-method="summaryMethod"
        :tree-props="{ children: propName }"
        :lazy="lazy"
        :load="load"
    >
        >
        <template #empty>
            <slot name="empty"></slot>
        </template>
        <template v-for="(item, index) in rows">
            <template v-if="rowSelector(index)">
                <el-table-column :key="item.label" :min-width="minWidth || null" :label="item.label" :prop="item.prop" v-bind="{ ...item.attrs }" />
            </template>
            <template v-else>
                <el-table-column :key="item.label || item.slot" v-slot="{ row }" :min-width="minWidth || null" :label="item.label" v-bind="{ ...item.attrs }">
                    <component :is="item.component" v-if="item.component" :row="row" :options="item.options"></component>
                    <slot v-else :name="item.slot" v-bind="row"></slot>
                </el-table-column>
            </template>
        </template>
    </el-table>
</template>

<script>
import { Table, TableColumn } from 'element-ui'
export default {
    name: 'VcTable',
    components: {
        'el-table': Table,
        'el-table-column': TableColumn
    },
    props: {
        data: {
            type: Array,
            required: true
        },
        rows: {
            type: Array,
            required: true
        },
        headerCellClasses: {
            type: String,
            default: ''
        },
        rowClassName: {
            type: String,
            default: ''
        },
        emptyText: {
            type: String,
            default: ''
        },
        minWidth: {
            type: String,
            default: ''
        },
        maxHeight: {
            type: String,
            default: '1080'
        },
        rowErrors: {
            type: Boolean,
            default: false
        },
        showSummary: {
            type: Boolean,
            default: false
        },
        sumText: {
            type: String,
            default: ''
        },
        summaryMethod: {
            type: Function,
            default: null
        },
        propName: {
            type: String,
            default: ''
        },
        currentId: {
            type: String,
            default: ''
        },
        lazy: {
            type: Boolean,
            default: false
        },
        load: {
            type: Function,
            default: () => {}
        }
    },
    methods: {
        rowSelector(index) {
            return !!this.rows[index].prop
        },
        styleRow({ rowIndex }) {
            return this.rowErrors
                ? this.rows.map((row) => {
                      if (row.shouldValidate && !this.data[rowIndex][row.prop]) {
                          this.$emit('error-row')
                          return 'error-row'
                      }
                      return null
                  })
                : null
        }
    }
}
</script>
<style lang="scss" scoped>
.el-table::v-deep .error-row {
    background: oldlace;
}
</style>
