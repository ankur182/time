package com.bnpp.asset.v2.domain.models.projectfinance;

import com.bnpp.asset.v2.domain.models.Page;
import com.bnpp.asset.v2.domain.models.Pageable;

import java.util.List;
import java.util.function.Function;
import java.util.stream.Collectors;

/**
 * Domain Page wrapper specifically for ProjectFinance pagination.
 */
public class PageProjectFinance implements Page<ProjectFinance> {

    private final List<ProjectFinance> content;
    private final Pageable pageable;
    private final long totalElements;

    public PageProjectFinance(List<ProjectFinance> content, Pageable pageable, long totalElements) {
        this.content = content;
        this.pageable = pageable;
        this.totalElements = totalElements;
    }

    @Override
    public long getTotalElements() {
        return totalElements;
    }

    @Override
    public List<ProjectFinance> getContent() {
        return content;
    }

    @Override
    public int getNumber() {
        return pageable.getPageNumber();
    }

    @Override
    public int getSize() {
        return pageable.getPageSize();
    }

    @Override
    public <R> Page<R> map(Function<ProjectFinance, R> contentTransform) {
        List<R> mappedContent = content.stream().map(contentTransform).collect(Collectors.toList());
        return new PageProjectFinanceGeneric<>(mappedContent, pageable, totalElements);
    }

    @Override
    public Pageable getPageable() {
        return pageable;
    }
}



-----

package com.bnpp.asset.v2.domain.models.projectfinance;

import com.bnpp.asset.v2.domain.models.Page;
import com.bnpp.asset.v2.domain.models.Pageable;

import java.util.List;
import java.util.function.Function;
import java.util.stream.Collectors;

/**
 * Generic implementation for Page.map()
 */
public class PageProjectFinanceGeneric<R> implements Page<R> {

    private final List<R> content;
    private final Pageable pageable;
    private final long totalElements;

    public PageProjectFinanceGeneric(List<R> content, Pageable pageable, long totalElements) {
        this.content = content;
        this.pageable = pageable;
        this.totalElements = totalElements;
    }

    @Override
    public long getTotalElements() {
        return totalElements;
    }

    @Override
    public List<R> getContent() {
        return content;
    }

    @Override
    public int getNumber() {
        return pageable.getPageNumber();
    }

    @Override
    public int getSize() {
        return pageable.getPageSize();
    }

    @Override
    public <T> Page<T> map(Function<R, T> contentTransform) {
        List<T> mappedContent = content.stream().map(contentTransform).collect(Collectors.toList());
        return new PageProjectFinanceGeneric<>(mappedContent, pageable, totalElements);
    }

    @Override
    public Pageable getPageable() {
        return pageable;
    }
}
