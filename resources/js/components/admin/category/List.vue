<template>
    <div>
        <!-- Main content -->
        <section class="content">
            <div class="row justify-content-around">
                <div class="col-8">
                <div class="card">
                    <div class="card-header">
                    <h3 class="card-title">Category List</h3>

                    <div class="card-tools">
                        <router-link to="/add-category" class="btn btn-primary">Add Category</router-link>
                    </div>
                    </div>
                    <!-- /.card-header -->
                    <div class="card-body">
                    <table id="example2" class="table table-bordered table-hover">
                        <thead>
                        <tr>
                        <th>S/N</th>
                        <th>Category Name</th>
                        <th>Date</th>
                        <th>Actions</th>
                        </tr>
                        </thead>
                        <tbody>
                        <tr v-for="(category,index) in getAllCategory" :key="category.id">
                        <td>{{ index+1 }}</td>
                        <td>{{ category.cat_name }}</td>
                        <td>{{ category.created_at | timeformat }}</td>
                        <td>
                            <router-link :to="`/edit-category/${category.id}`">Edit</router-link>
                            <a href=""  @click.prevent="deleteCategory(category.id)">Delete </a>
                        </td>
                        </tr>
                        </tbody>
                    </table>
                    </div>
                    <!-- /.card-body -->
                </div>
                <!-- /.card -->
                </div>
                <!-- /.col -->
            </div>
            <!-- /.row -->
        </section>
        <!-- /.content -->
    </div>
</template>

<script>
export default {
    name: "List",
    mounted(){
        this.$store.dispatch("allCategory")
    },
    computed:{
        getAllCategory(){
            return this.$store.getters.getCategory
        }
    },
    methods:{
        deleteCategory(id){
            axios.get('/category/'+id)
                .then(()=>{
                    this.$store.dispatch("allCategory")
                     Toast.fire({
                        type: 'success',
                        title: 'Category Deleted successfully'
                    })     
                })
                .catch(()=>{
                           
                })
        }
    }
}
</script>

<style scoped>

</style>