# Pacote PKG_PROFESSOR

## Descrição
O pacote `PKG_PROFESSOR` contém procedures e funções que implementam operações relacionadas à entidade Professor. As principais funcionalidades incluem listar o total de turmas por professor, calcular o total de turmas de um professor específico e obter o nome do professor responsável por uma disciplina.

## Conteúdo do Pacote

### Cursor para Total de Turmas por Professor
**Nome:** `C_TOTAL_TURMAS_PROFESSOR`

**Descrição:** 
Lista os nomes dos professores e o total de turmas que cada um leciona. Exibe apenas os professores que são responsáveis por mais de uma turma.

**Exemplo de Uso:**
```sql
DECLARE
  CURSOR C_TOTAL_TURMAS_PROFESSOR IS
    SELECT P.NOME, COUNT(T.ID) AS TOTAL_TURMAS
    FROM PROFESSORES P
    JOIN TURMAS T ON P.ID = T.ID_PROFESSOR
    GROUP BY P.NOME
    HAVING COUNT(T.ID) > 1;
BEGIN
  FOR R_PROFESSOR IN C_TOTAL_TURMAS_PROFESSOR LOOP
    DBMS_OUTPUT.PUT_LINE('Professor: ' || R_PROFESSOR.NOME || ', Total de Turmas: ' || R_PROFESSOR.TOTAL_TURMAS);
  END LOOP;
END;
/

