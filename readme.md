# InferWiki, inferential benchmark for Knowledge Graph completion

This is the dataset of the paper *Are Missing Links Predictable? An Inferential Benchmark for Knowledge Graph Completion* in ACL'21.

# Datasets

We use two datasets: InferWiki16k and InferWiki64k, where InferWiki16k is a subset of InferWiki64k.

## InferWiki16k

The main files for InferWiki16k include:

```
16k
│   ent_vocab.txt
│   rel_vocab.txt
│   test_neg.txt
│   test_pos.txt
│   train.txt
│   valid_neg.txt 
│   valid_pos.txt
```

For each of the file, the format is:

### ent_vocab.txt

'Entity_id' '\t\t' 'Count' '\t\t' 'Entity_name' '\t\t' 'Aliases (splited by \t)'

### rel_vocab.txt

'Relation_name' '\t\t' 'Count'

### test_neg.txt & valid_neg.txt for testing and development, respectively

'Entity_id'  '\t' 'Relation_name' '\t' 'Entity_id' '\t' 'Label'

> where the 'Label' for all the following negatives has four types:
> - **-1c**, Manually verified negatives, we can find conflicting triples from training set.
> - **-1**, Unverified nagatives, we can automatically detect conflicting triples from training set.
> - **0c**, Unknown when adopting *Open-world assumption*, which are manually verified nagatives (*Closed-world assumption*), but cannot find conflicting triples from training set.
> - **r**, Negatives by randomly corruption the head or tail entity

### test_pos.txt & valid_pos.txt for testing and development, respectively

'Entity_id'  '\t' 'Relation_name' '\t' 'Entity_id' '\t' 'Relation type' '\t' 'Inference pattern' '\t' 'Path length'

> where:
> - **Relation type** is one of ['1-1', '1-n', 'n-1', 'n-n'], denoting the ratio of head entity to tail entity for each relation type.
> - **Inference pattern** has five types :
>   - P1: Symmetry
>   - P2: Inversion
>   - P3:Hierarchy
>   - P4: Intersection
>   - P5: Composition
>   - P0: others
> - **Path length**, the number of hops for the inferential paths, that is, how many training triples consist of the path for the testing triple. There may be multiple paths for one testing triple, separated by ','.

### train.txt

'Entity_id'  '\t' 'Relation_name' '\t' 'Entity_id'

## InferWiki64k

InferWiki64k has the same format with InferWiki16k, except an additional file:

### neg_with_conflict.txt

'index' '\t' 'Entity_id'  '\t' 'Relation_name' '\t' 'Entity_id' '\t' 'Label' '-/+'

> where:
> 'Label' is the same with that in test_neg.txt
> '-/+' denotes negatives and the corresponding conflicting triples

## Reference
If you use our code, please cite our paper:
```
@inproceedings{cao2021are,
  title={Are Missing Links Predictable? An Inferential Benchmark for Knowledge Graph Completion},
  author={Yixin Cao, Xiang Ji, Xin Lv, Juanzi Li, Yonggang Wen and Hanwang Zhang.},
  booktitle={ACL},
  year={2021}
}
```