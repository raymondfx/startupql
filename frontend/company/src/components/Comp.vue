<template>

  <div>
    <table class="table table-striped mt-4">
      <thead>
      <tr>
        <th scope="col">name</th>
        <th scope="col">title</th>
        <th scope="col">city</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="input in directory.edges" :key="input.id">
        <td>{{ input.node.employeeName }}</td>
        <td>{{ input.node.employeeTitle.titleName }}</td>
        <td>{{ input.node.employeeCity.cityName }}</td>
      </tr>
      </tbody>
    </table>
  </div>

</template>

<script>
  import axios from 'axios'
  export default{
  	name: 'CompanyData',
    data(){
      return {
      	directory: []
      }
    },
    async mounted () {
    	try {
	var result = await axios({
		method: 'POST',
		url: 'http://127.0.0.1:8000/graphql/',
		data: {
			query: `
			{
			  allEmployees {
			    edges {
			      node {
				id
				employeeName
				employeeTitle {
				  titleName
				}
				employeeCity {
				  cityName
				}
			      }
			    }
			  }
			}
			`
    			}
    		})
    		this.directory = result.data.data.allEmployees
    	} catch (error) {
    		console.error(error)
    	}
    }
  }
</script>

<style scoped>
</style>