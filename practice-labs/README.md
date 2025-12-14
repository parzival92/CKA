# Practice Labs

Hands-on labs to practice each domain covered in the CKA exam.

## Lab Structure

Each lab folder contains:
- `README.md`: Lab objectives and instructions
- `setup.sh`: Setup script to create resources
- `cleanup.sh`: Cleanup script to remove resources
- `solutions/`: Step-by-step solutions

## Labs

### Lab 1: Basic Cluster Setup
**Topics**: Cluster architecture, nodes, basic kubectl

**Objectives**:
- Create a multi-node cluster
- Understand cluster components
- Practice basic kubectl commands

### Lab 2: Deployments & Workloads
**Topics**: Deployments, scaling, rolling updates

**Objectives**:
- Create deployments
- Scale applications
- Perform rolling updates
- Implement rollbacks

### Lab 3: Networking & Services
**Topics**: Services, ingress, network policies

**Objectives**:
- Expose applications with different service types
- Configure ingress
- Implement network policies

### Lab 4: Storage
**Topics**: PV, PVC, storage classes

**Objectives**:
- Create persistent volumes
- Create persistent volume claims
- Use storage classes for dynamic provisioning

### Lab 5: Troubleshooting
**Topics**: Debugging, logging, diagnostics

**Objectives**:
- Debug pod issues
- Troubleshoot networking
- Analyze cluster problems
- Fix application failures

## How to Use

1. Read the lab README
2. Follow the instructions
3. Attempt the tasks without looking at solutions
4. Compare your solution with the provided answer
5. Run cleanup script before moving to next lab

## Getting Help

If stuck:
1. Check official Kubernetes documentation
2. Review the Quick Reference guides
3. Look at manifest templates
4. Review troubleshooting checklist
