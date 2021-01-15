# k8-yaml-cleaner
Nodejs script, to help cleanup a YAML dump from kubernetes to a more usable importable script  (into another cluster)

# Use case
Got a kubernetes cluster you need to migrate to another cluster (or backup). But do not have any of the existing yaml definition file.

Well this script is just for you .... Sort of ...

# Step 1 - Export your existing yaml definition

```
kubectl get deployment,service,pod yourapp -o yaml --export
kubectl get deploy --all-namespaces -o yaml --export
```

Problem is, this exports the existing k8 state - not the yaml you previously imported. And in addition, it has so much auxillary information unique to the current cluster, that the import command will fail on a new k8 cluster.

# Step 2 - Filter the data for junk

```
node ./yaml-cleaner.js -file <filepath>
```

**Disclaimer:** This is a really hacky script, it probably will not work 100% for you, you may need to modify the script, or hand tune/scrub the data.

# Step 3 - Import, Fail, Handtune

See disclaimer, in step 2 - adjust your yaml, until its usuable / importable

# Step 4 - BACKUP

You do not want to repeat this whole process again.
