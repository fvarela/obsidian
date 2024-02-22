Installation:
	pip install luigi

Tasks
	A task should be
		Atomic
		Idempotent (same result every time you run it)
	Tres componentes principales (acrónimo ROR):
		Requires - Dependencies
		Output - Target
		Run - Logic

WrapperTask
	Tipically the WrapperTask is at the end of the pipeline.
	It does not produce any output of tis own but is used to trigger other tasks.
	Tthe WrapperTask uses the yield in its run method or requires method to generate the tasks it depends on
	Overview:
		Is a special kind of task designed to bundle together a collection of tasks. It doesn't produce any output itself; instead, it is considered complete when all the tasks it "wraps" (i.e., the tasks it requires) are complete. Here's how it works
	Task generation goes in 'requires' method:
		When Luigi runs a task, it first calls the requires method to determine what other tasks need to be complete before it can run. In the case of a WrapperTask, the requires method returns a list of other tasks, without doing any processing itself.
	Task completion:
		The WrapperTask (i.e., AllFilesProcessed) doesn't have its own output method because it doesn't produce any output of its own. Instead, it's considered complete when all the tasks returned by its requires method are complete. 
	Best practices
		Avoid putting the logic in the requires method as luigi may call this function several times. Use run instead.


Scheduler:

local scheduler
	```
	if __name__ == '__main__':
		luigi.run(['HelloWorld', '--local-scheduler'])```

luigid (Central scheduler)

