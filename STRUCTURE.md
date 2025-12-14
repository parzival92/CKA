# CKA Study Repository Structure

## Directory Overview

```
CKA/
├── 1-cluster-architecture/    # 25% of exam
│   ├── README.md
│   ├── examples/              # Practical examples
│   └── yaml-files/            # YAML templates
│
├── 2-workloads-scheduling/    # 15% of exam
│   ├── README.md
│   ├── examples/
│   └── yaml-files/
│
├── 3-services-networking/     # 20% of exam
│   ├── README.md
│   ├── examples/
│   └── yaml-files/
│
├── 4-storage/                 # 10% of exam
│   ├── README.md
│   ├── examples/
│   └── yaml-files/
│
├── 5-troubleshooting/         # 30% of exam (MOST IMPORTANT!)
│   ├── README.md
│   ├── examples/
│   ├── scenarios/             # Real-world troubleshooting scenarios
│   └── yaml-files/
│
├── quick-reference/           # Quick lookups during study
│   ├── kubectl-commands.md
│   ├── manifests-templates.yaml
│   └── troubleshooting-checklist.md
│
├── practice-labs/             # Hands-on practice
│   ├── lab-1-basic-setup/
│   ├── lab-2-deployments/
│   ├── lab-3-networking/
│   ├── lab-4-storage/
│   └── lab-5-troubleshooting/
│
├── practice-exams/            # Mock exams
│   ├── mock-exam-1/
│   ├── mock-exam-2/
│   └── answers/
│
├── README.md                  # Main overview
├── STRUCTURE.md               # This file
└── docs/
    └── Commands.md            # Kubectl cheat sheet

```

## Study Path Recommendation

### Phase 1: Learn Fundamentals (Week 1-2)
1. Read `README.md` for exam overview
2. Study each domain folder in order (1-5)
3. Review `quick-reference/` frequently

### Phase 2: Practice (Week 3-4)
1. Complete practice labs (lab-1 through lab-5)
2. Work through real-world scenarios
3. Reference troubleshooting checklist

### Phase 3: Final Prep (Week 5)
1. Take mock exams under timed conditions
2. Review weak areas
3. Practice troubleshooting scenarios

### Exam Day
- Have `quick-reference/kubectl-commands.md` memorized
- Remember: Troubleshooting is 30% of exam
- Practice time management

## Key Stats

| Domain | Weight | Focus |
|--------|--------|-------|
| Troubleshooting | 30% | ⭐ Most Important |
| Cluster Architecture | 25% | Core Skills |
| Services & Networking | 20% | Common Tasks |
| Workloads & Scheduling | 15% | Practical |
| Storage | 10% | Specialized |

## Getting Started

1. Check the README.md in each domain folder
2. Start with 1-cluster-architecture
3. Use examples/ folder for hands-on learning
4. Reference quick-reference/ often
5. Practice with practice-labs/

## Useful Commands

```bash
# Navigate to any domain
cd 1-cluster-architecture

# View structure
tree -L 2

# Search for topics
grep -r "topic" .

# View all examples
ls -la */examples/
```

## Tips for Success

✅ **Do**:
- Practice hands-on with real clusters
- Focus on troubleshooting (30% of exam)
- Memorize common kubectl commands
- Understand YAML manifest structure
- Read official Kubernetes documentation

❌ **Don't**:
- Only read, practice instead
- Memorize all commands
- Skip network policies
- Ignore storage topics
- Cram the night before

## Resources

- [Official Kubernetes Docs](https://kubernetes.io/docs/)
- [Kubernetes Blog](https://kubernetes.io/blog/)
- [CKA Exam Details](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/)
