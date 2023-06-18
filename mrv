def select_unassigned_variable(variables, assignment):
    unassigned_vars = [var for var in variables if var not in assignment]
    return min(unassigned_vars, key=lambda var: len(variables[var]))

def is_assignment_complete(assignment, variables):
    return len(assignment) == len(variables)

def is_consistent(variable, value, assignment, constraints):
    for constraint in constraints[variable]:
        if constraint[0] in assignment and assignment[constraint[0]] == value:
            return False
    return True

def mrv(variables, domain, constraints):
    assignment = {}
    return backtrack(assignment, variables, domain, constraints)

def backtrack(assignment, variables, domain, constraints):
    if is_assignment_complete(assignment, variables):
        return assignment

    var = select_unassigned_variable(variables, assignment)
    for value in domain[var]:
        if is_consistent(var, value, assignment, constraints):
            assignment[var] = value
            result = backtrack(assignment, variables, domain, constraints)
            if result is not None:
                return result
            del assignment[var]
    return None
