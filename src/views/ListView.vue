<template>
    <h1>리스트가져오기</h1>

    <table border="1">
        <colgroup>
            <col style="width: 40px;">
            <col style="width: 70px;">
            <col style="width: 150px;">
            <col style="width: 160px;">
            <col style="width: 40px;">
        </colgroup>
        <thead class="gray">
            <tr>
                <th>번호</th>
                <th>이름</th>
                <th>핸드폰</th>
                <th>회사</th>
                <th>성별</th>
            </tr>
        </thead> 
        <tbody>
            <tr v-for="(personVo, i) in personList" v-bind:key="i">
                <td>{{ personVo.no }}</td>
                <td>{{ personVo.name }}</td>
                <td>{{ personVo.hp }}</td>
                <td>{{ personVo.company }}</td>
                <td>{{ personVo.gender }}</td>
            </tr>
        </tbody>
    </table>
</template>

<script>
import axios from 'axios';

export default{
    name : 'ListView',
    components : {},
    data(){
        return {
            personList : []
        };
    },
    methods : {
        getList(){
            axios({
                method: 'get',
                url: 'https://raw.githubusercontent.com/clz2024-red/api/main/person.json',
                headers: { "Content-Type": "application/json; charset=utf-8" },
                responseType: 'json'
            }).then(response => {
                this.personList = response.data;
            }).catch(error => {
                console.log(error);
            });
        }
    },
    created (){
        this.getList();
    }
}
</script>

<style>
table {
    text-align: center;
    border: 1px solid #000000;
    border-collapse: collapse;
}

.gray {
    background-color: #d6d6d6;
}
</style>