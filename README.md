# k8-yaml-cleaner
Nodejs script, to help cleanup a YAML dump from kubernetes to a more usable importable script  (into another cluster)

## Use case
Got a kubernetes cluster you need to migrate to another cluster (or backup). But do not have any of the existing yaml definition file.

- Bad news: I spent days, only to find out that k8 does **not** retain the original yamls you imported
- Good news: You can export the existing definitions, in full as yaml ...

Well this script is just for you .... Sort of ...

### Step 1 - Export your existing yaml definition

```
kubectl get deployment,service,pod yourapp -o yaml --export
kubectl get deploy --all-namespaces -o yaml --export
```

Problem is, this exports the existing k8 state - not the yaml you previously imported. 

In addition, it has so much auxillary information unique to the current cluster, inflating what was previously a 50 line yaml, to a 250 line yaml - to the extent, that the import command will fail on a new k8 cluster. 

### Step 2 - Filter out junk data
```
node ./yaml-cleaner.js -file <filepath>
```

**Disclaimer:** This is a really hacky script, it uses regex, it probably will not work 100% for you, but serves as a starting point, in making the YAML sane and human - While unlikely, it might even filter out critical/useful data.

### Step 3 - Import, Fail, Test, Handtune

See disclaimer, in step 2 - adjust your yaml, until its usuable / importable

### Step 4 - BACKUP

You do not want to repeat this whole process again. 

---

I apologies if the script isn't good enough for your use case, please send patches, or if your hardworking enough consider adding in a real YAML parser (instead of this evil regex search and replace).

Hopefully it will help the next person, who will go through this.
