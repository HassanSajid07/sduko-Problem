def select_unassigned_variable_mrv(variables, assignment, domain):
    unassigned_vars = [var for var in variables if var not in assignment]
    return min(unassigned_vars, key=lambda var: len(domain[var]))

def is_assignment_complete(assignment, variables):
    return len(assignment) == len(variables)

def is_consistent(variable, value, assignment, constraints):
    for constraint in constraints[variable]:
        if constraint[0] in assignment and assignment[constraint[0]] == value:
            return False
    return True

def forward_check(variable, value, assignment, constraints, domain):
    for constraint in constraints[variable]:
        if constraint[0] in assignment:
            continue
        updated_domain = domain[constraint[0]][:]  # Create a copy of the domain
        updated_domain = [val for val in updated_domain if is_consistent(constraint[0], val, assignment, constraints)]
        if len(updated_domain) == 0:
            return False
        domain[constraint[0]] = updated_domain
    return True

def fc_mrv(variables, domain, constraints):
    assignment = {}
    return fc_mrv_backtrack(assignment, variables, domain, constraints)

def fc_mrv_backtrack(assignment, variables, domain, constraints):
    if is_assignment_complete(assignment, variables):
        return assignment

    var = select_unassigned_variable_mrv(variables, assignment, domain)
    for value in domain[var]:
        if is_consistent(var, value, assignment, constraints):
            assignment[var] = value
            updated_domain = domain.copy()
            if forward_check(var, value, assignment, constraints, updated_domain):
                result = fc_mrv_backtrack(assignment, variables, updated_domain, constraints)
                if result is not None:
                    return result
            del assignment[var]
    return None
