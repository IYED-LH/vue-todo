<template>

    <form @submit="onSubmit" class="form-container">

        <div class="field padding-bottom--24">
                  
            <label for="task">Task</label>
            <input type="text" v-model="title" class="form-control" name="title" placeholder="add a task">
                
        </div>
                
        <div class="field padding-bottom--24">
                  
            <label for="date">Date & Time</label>
            <input v-model="date" type="datetime-local" name="Date">
                
        </div>


        <div class="field field-checkbox padding-bottom--24 flex-flex align-center">
                 
                  <label for="checkbox">
                    <input type="checkbox" v-model="completed" name="completed"> Task Completed?
                  </label>
                
        </div>
                
        <div class="field padding-bottom--24">
                 
                  <input type="submit" name="submit" value="Save Task">
        </div>
                
    </form>
  
</template>

<script>

export default {
    name: 'AddTask',
    data() {
      return {
        title: '',
        date: '',
        completed: false
      }
    },
    methods:{

        onSubmit(e) {
            e.preventDefault()

            if ((!this.title) || (!this.date)) {
                alert('Please add a task')
                return
            }

            const newtask = {
                id: Math.floor(Math.random() * 100000),
                title: this.title,
                date: this.date,
                completed: this.completed 
                }

            this.$emit('add-task', newtask)
            
            this.title = ''
            this.date = ''
            this.completed = false
            
            }   
        }
    }

</script>


<style scoped> 

.form-container {
  margin-bottom: 24px;
}

.padding-bottom--24 {
  padding-bottom: 24px;
}


label {
    margin-bottom: 10px;
}

.reset-pass a,label {
    font-size: 14px;
    font-weight: 600;
    display: block;
}
.reset-pass > a {
    text-align: right;
    margin-bottom: 10px;
}


.field input {
    font-size: 16px;
    line-height: 28px;
    padding: 8px 16px;
    width: 100%;
    min-height: 44px;
    border: unset;
    border-radius: 4px;
    outline-color: rgb(84 105 212 / 0.5);
    background-color: rgb(255, 255, 255);
    box-shadow: rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(60, 66, 87, 0.16) 0px 0px 0px 1px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px, 
                rgba(0, 0, 0, 0) 0px 0px 0px 0px;
}

input[type="submit"] {
    background-color: rgb(27, 27, 27);
    color: #fff;
    cursor: pointer;
}
.field-checkbox input {
    width: 20px;
    height: 15px;
    margin-right: 5px; 
    box-shadow: unset;
    min-height: unset;
}
.field-checkbox label {
    display: flex;
    align-items: center;
    margin: 0;
}

</style>