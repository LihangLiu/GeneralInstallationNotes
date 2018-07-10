# GeneralInstallationNotes
Some notes of solutions for installing problems

# tensorflow
## install cuDNN locally
	  "extract compressed file"
	  export LD_LIBRARY_PATH=~/repos/cuDNN:$LD_LIBRARY_PATH
	  export LD_LIBRARY_PATH=~/repos/cuDNN/lib64:$LD_LIBRARY_PATH

## install bazel locally:
	  git clone https://github.com/bazelbuild/bazel.git
	  git checkout 0.4.4 			# $BAZEL_VERSION
	  cd bazel
	  bazel build //src:bazel
	  export PATH=~/repos/bazel/bazel-bin/src:$PATH

## error: invalid command 'bdist_wheel'
	  pip install --user wheel

# sshfs
## mount
	sudo sshfs -o allow_other,defer_permissions leonliu@eldar-1.cs.utexas.edu:/u/leonliu/repos  ~/eldar-1/
	
## unmount 
	sudo umount ~/eldar-1

# sublime
## auto-complete from other files

	import sublime_plugin, sublime

	class AutocompleteAll(sublime_plugin.EventListener):

    	def on_query_completions(self, view, prefix, locations):
        	window = sublime.active_window()
	        # get results from each tab
        	results = [v.extract_completions(prefix) for v in window.views() if v.buffer_id() != view.buffer_id()]
	        results = [(item,item) for sublist in results for item in sublist] #flatten
        	results = list(set(results)) # make unique
	        results.sort() # sort
        	return results

