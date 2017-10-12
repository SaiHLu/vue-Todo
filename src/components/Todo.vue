<template>
  <div id="todo" class="container col-md-6 col-md-offset-3">
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>
          Todo Tasks <span class="pull-right">({{calculateNo()}})</span>
        </h3>
      </div>
      <div class="panel-body">
        <ol>
          <li  v-for="(task, index) in tasks" v-bind:key="task.id">
            {{task.title}}<span class="pull-right dd" v-on:click="remove(index)">&times;</span>
          </li>
        </ol>
      </div>
      <div class="panel-footer">
          <div class="col-md-2">
            <label for="job" class="control-label">New Job</label>
          </div>
          <div class="col-md-8"><input type="text"  ref="jobs" id="job"  v-on:keyup.enter="add" class="form-control col-md-2" placeholder="Enter new tasks" autofocus></div>
          <button type="submit" v-on:click="add" class="btn btn-info">Add</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  data () {
    return {
      tasks: [
        {id: 1, title: 'Reading'},
        {id: 2, title: 'Writing'},
        {id: 3, title: 'Playing'},
        {id: 4, title: 'Watching'},
        {id: 5, title: 'Eating'},
        {id: 6, title: 'Sleeping'}
      ],
      nextTodoId: 7
    }
  },
  methods: {
    remove: function(index){
      // console.log(index);
      this.tasks.splice(index, 1);
    },
    add: function(){
      this.tasks.push( { id: this.nextTodoId, title: this.$refs.jobs.value } );
      this.$refs.jobs.value = "";
      this.$refs.jobs.autofocus = true;
      this.nextTodoId++;
    },
    calculateNo: function(){
      return this.tasks.length;
    }
  },
  created: function() {
    // console.log(this.$refs);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  div.container {
    margin-top: 50px;
  },
  span.dd {
    cursor: pointer;
  }
</style>
