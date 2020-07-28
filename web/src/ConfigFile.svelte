<style>
 .config-file {
		 width: 300px;
		 border: 1px solid #aaa;
		 border-radius: 2px;
		 box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
		 padding: 1em;
 }

 h2 {
		 padding: 0 0 0.2em 0;
		 margin: 0 0 1em 0;
		 border-bottom: 1px solid #ff3e00
 }

 .reviewer, .approver, label {
		 padding: 0 0 0 1.5em;
		 background:  0 0 no-repeat;
		 background-size: 20px 20px;
		 margin: 0 0 0.5em 0;
		 line-height: 1.2;
 }

 .reviewer{ background-image: url(/icons/person.svg) }
 .approver{ background-image: url(/icons/person.svg) }
 .label{ background-image: url(/icons/label.svg) }
 .missing { color: #999 }
</style>

<article class="config-file">
	  <h2>
		    <slot name="name">
			      <span class="missing">Unknown config file</span>
		    </slot>
	  </h2>

	  <div class="reviewers">
		    <slot name="reviewer">
			      <span class="missing">No reviewers</span>
		    </slot>
	  </div>

	  <div class="approvers">
		    <slot name="approver">
			      <span class="missing">No approver</span>
		    </slot>
	  </div>

	  <div class="labels">
		    <slot name="label">
			      <span class="missing">No labels</span>
		    </slot>
	  </div>

</article>
