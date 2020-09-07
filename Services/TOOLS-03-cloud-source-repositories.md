# Cloud Source Repositories

- **first way** : use hosted Git repo, less management and less work, but limited control.
- **second way** : self hosted Git repo, more responsibility in managing those repositories.

- with Cloud you have the third way: **Hosted on GCP, managed by google, and protected by IAM rules**
  - we can create any number of private repositories.
  - The code can be pulled in compute engines, App engine and GKE.
  - Also provide a **source viewer**, where we can view the files available in the managed Git repo.

- Benefits
  - consistent security system using IAM.
  - private Git Repo.
  - Managed by Google
  - Scalable
  - extends standard git workflow to cloud build, cloud pub/sub an compute services.
  - close to build and deployment env reducing latency.
  - Mirror from public GitHub and BitBucket.
  - unlimited private Git Repo are supported.
  - Integrated regex based code search.
  