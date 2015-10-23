#webportfolio-rq-worker

Creates a simple worker to add job, start worker etc

## Install

    pip install webportfolio-rq-worker
    
## Usage

    # extras.py
    
    from webportfolio import WebPortfolio
    import webportfolio_rq_worker as wp_rq_worker
    
    rq_worker = wp_rq_worker.RQ_Worker()
    WebPortfolio.bind(rq_worker)
    
    
    # views.py
    
    import extras
    
    @extras.rq_worker.job
    def hello():
        pass
        
    def hi():
        data = {}
        job = extras.rq_worker.add_job(callback, **data)
        job_id = job.id
        
    def callback(data):
        pass
        
    def my_job():
        job_id = "xxxxx"
        job = extras.rq_worker.get_job(job_id)
        
        
    # manager.py
    
    import extras
    
    # run the worker
    extras.rq_worker.run()