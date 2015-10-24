#webportfolio-rq-worker

Creates a simple worker to add job, start worker etc

## Install

    pip install webportfolio-rq-worker
    
## Usage

    # config.py
    
    class Config(object):
        
        RQ_WORKER_URI = ""  # The redis uri
        RQ_WORKER_NAME = "default"  # The name of the worker
        RQ_WORKER_TTL = 600  # TTL
        RQ_WORKER_RESULT_TTL = 7200  # How long the results stay in
    
    
    # extras.py
    
    from webportfolio import WebPortfolio
    import webportfolio_rq_worker as wp_rq_worker
    
    rq_worker = wp_rq_worker.RQ_Worker()
    WebPortfolio.bind(rq_worker)
    
   
    # views.py
    
    import extras
            
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
    
    import webportfolio_rq_worker as wp_rq_worker
    
    rq_worker = wp_rq_worker.RQ_Worker(uri="***")
    
    # run the worker
    rq_worker.run()