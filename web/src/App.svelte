<!-- https://eugenkiss.github.io/7guis/tasks#crud -->

<style>
 header {
     padding: 2rem;
     align: center;
 }
 main {
     display: grid;
     padding: 2rem;
     grid-template-columns: minmax(150px, 10%) 1fr;
     height: 50vh
 }

 input {
		 display: block;
		 margin: 0 0 0.5em 0;
 }

 footer {
     padding: 2rem;
     text-align: center;
 }

 select,textarea {
     width: 90%;
     padding: 10px;
     height: 60vh;
 }

 label {
     white-space: pre-wrap;
     font-size: small; 
 }

</style>
<script>
 let configFiles = [
     {
         path: '/A/OWNERS',
         content: `AAA# See the OWNERS docs at https://go.k8s.io/owners

     filters:
     ".*":
     reviewers:
     - robertkielty
     - dchen1107
     - lavalamp
     - smarterclayton
     - thockin
     - liggitt
     approvers:
     - bgrant0607
     - brendandburns
     - dchen1107
     - lavalamp
     - smarterclayton
     - thockin
     - wojtek-t
     - liggitt
     emeritus_approvers:
     - jbeda

     # go.{mod,sum} files relate to go dependencies, and should be reviewed by the
     # dep-approvers
     "go\\.(mod|sum)$":
     required_reviewers:
     - kubernetes/dep-approvers
     labels:
     - area/dependency
     # metrics.go files are sig-instrumentation related, and should be tagged
     # and reviewed by sig-instrumentation
     "metrics\\.go$":
     labels:
     - sig/instrumentation
         `},
     {
         path: '/B/OWNERS',
         content: `BBB See the OWNERS docs at https://go.k8s.io/owners

     reviewers:
     - michellecraughwell
     - brendandburns
     - dchen1107
     - lavalamp
     - smarterclayton
     - thockin
     approvers:
     - brendandburns
     - dchen1107
     - lavalamp
     - smarterclayton
     - thockin

         `}

 ];
 let searchTerm = '';
 let path = '';
 let content ='';
 let i = 0;
 let filteredConfigFiles = null ;
 $: i
 $: filteredConfigFiles = searchTerm
                        ? configFiles.filter(configFile => {
                            const searchable =`${configFile.path} ${configFile.content}`;
                            return searchable.toLowerCase().includes(searchTerm.toLowerCase());
                        }) : configFiles ;
 $: selectedConfigFile = filteredConfigFiles[i];
 $: reset_textarea(selectedConfigFile)

 function reset_textarea(configFile){
     if (configFile) {
         content=configFile.content
     } else {
         content=null
     }
 }

</script>

<header>
    <h1>Koral</h1>
    <h2>find where reviewers, approvers and labels are configured</h2>
    <label for="srch">Search for paths to OWNER config files, reviewer and approver usernamesa or pull request labels </label>
    <input id="srch" size={80} placeholder="paths reviewers approvers labels" bind:value={searchTerm}>
</header>
<main>
    <div>
        <select bind:value={i} size={10}>
            {#each filteredConfigFiles as configFile, i}
                <option value={i}>{i} - {configFile.path}</option>
            {/each}
        </select>
    </div>
    <div>
        <textarea id="content_ta" bind:value={content}/>
    </div>
</main>
<footer>koral - Kubernetes owners reviewer approvers lister</footer>
