<script>
    export let courseGoal = ""
    
</script>

<style>
    .red {
        color: red;
    }
</style>

<h1>Assignment</h1>

<p>Solve these tasks.</p>

<ol>
  <li>Add an input field that allows users to enter a course courseGoal.</li>
  <li>Output the user input in a h1 tag.</li>
  <li>
    Color the output red (e.g. by adding a class) if it contains at least one exclamation mark.
  </li>
  <li>
    Put the h1 tag + output into a separate component to which you pass the user input
  </li>
</ol>


<h1>Course courseGoal: <span class="{courseGoal.includes("!") ? "red": null}">{courseGoal}</span></h1>
