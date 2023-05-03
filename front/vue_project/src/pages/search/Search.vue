<template>
    <div>
        <button @click="search" type="button" class="btn btn-primary">検索</button>
        <button @click="delete_data" type="button" class="btn btn-danger">削除</button>
       

        <table class="table">
            <thead>
                <tr>
                <th scope="col">ID</th>
                <th scope="col">ユーザ名</th>
                </tr>
            </thead>
            <tbody>   
                <tr  v-for="item in items" :key="item.message">
                    <th scope="row">{{item.id}}</th>
                    <td>{{item.name}}</td>
                </tr>   
            </tbody>
        </table>
    </div>
</template>
<script>
    import axios from 'axios';
    export default {
        data(){
            return{
                items: []
            }
        },
        methods: {
            search (){
                axios
                .get('https://jsonplaceholder.typicode.com/users')
                .then(
                    response => {
                        for (let i=0; i<response.data.length; i++) {
                            this.items.push(response.data[i]);
                        }
                        console.log(this.items);
                    } 
                ).catch(
                    error => {
                        let errorData1 = {id: 11, name: "Error Tarou"};
                        let errorData2 = {id: 12, name: "Error Jirou"};
                        this.items.push(errorData1);
                        this.items.push(errorData2);
                    }
                );
            },
            delete_data(){//method名 "delete" は予約語なので、"delete_data" に変更
                this.items.splice(0);//全てのデータを削除

            },
        }
    }
</script>