<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12" >
                <div class="col-md-6 col-sm-6" style="margin-top:20px;">Total {{total}} records</div>
                <table class="table">
                    <tr>
                        <th>id</th>
                        <th>name</th>
                        <th>email</th>
                    </tr>
                    <tr v-for="user in users" >
                        <td>{{user.id}}</td>
                        <td>{{user.name}}</td>
                        <td>{{user.email}}</td>
                    </tr>
                </table>
                <pagination 
                  :total="total" 
                  :per_page= "per_page" 
                  :current_page= "current_page" 
                  :last_page= "last_page" 
                  :next_page_url= "next_page_url" 
                  :prev_page_url= "prev_page_url" 
                  :from= "from" 
                  :to= "to" 
                ></pagination>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return{
                n:0,
                users: [],
                message:'Welcome',
                total: 0,
                per_page: 0,
                current_page: 0,
                last_page: 0,
                next_page_url: "",
                prev_page_url: "",
                from: 0,
                to: 0,
                q:""

            }
            
        },
        mounted() {
            let $this = this;
            axios.get('/user')
              // .then(response=>this.users = response.data)
              .then(function (response){
                $this.users = response.data.data
                $this.total = response.data.total
                $this.per_page = response.data.per_page
                $this.current_page = response.data.current_page
                $this.last_page = response.data.last_page
                $this.next_page_url = response.data.next_page_url
                $this.prev_page_url = response.data.prev_page_url
                $this.from = response.data.from
                $this.to = response.data.to

              })
              .catch(function (error) {
                console.log(error);
              });
        },
        methods:{
          toPage(n){
            let $this = this;
            axios.get('/user?page='+n)
            .then(function (response){
                $this.users = response.data.data
                $this.total = response.data.total
                $this.per_page = response.data.per_page
                $this.current_page = response.data.current_page
                $this.last_page = response.data.last_page
                $this.next_page_url = response.data.next_page_url
                $this.prev_page_url = response.data.prev_page_url
                $this.from = response.data.from
                $this.to = response.data.to
              })
              .catch(function (error) {
                console.log(error);
              });
          }
        }
    }

</script>
