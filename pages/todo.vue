<template>
    <b-container>
        <b-input-group prepend="タスク名">
            <b-form-input v-model="taskname"></b-form-input>
            <b-input-group-append>
            <b-button variant="outline-success" @click="addtask">タスク追加</b-button>
            </b-input-group-append>
        </b-input-group>
        <b-table striped hover :items="tasks" :fields="fields">
            <template #cell(date)=date>
                <p>{{date.value.toLocaleString()}}</p>
            </template>
            <template #cell(action)=task>
                <b-button size="sm" @click="completetask(task)" class="mr-2">
                    完了
                </b-button>
            </template>
        </b-table>
    </b-container>
</template>

<script>
export default {
    data() {
        return{
            tasks:[],
            fields: [{key: 'isActive',sortable: true},{key: 'date',sortable: true}, 'name', 'action'],
            taskname:""
        }
    },
    methods:{
        addtask() {
            let obj = {
                isActive : true,
                name : this.taskname,
                date : new Date()
            }
            this.tasks.push(obj);
        },
        completetask(task) {
            task.item.isActive = false;
        }
    }
}
</script>