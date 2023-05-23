# kempil87.github.io

**customHook for prepare url (useUrlParams) **

import { type Path, useLocation, useSearchParams } from 'react-router-dom';
export type Pathname = Pick<Path, 'pathname'>;
export interface UsePrepareUrlParams extends Pathname {
  params: Array<Record<string, string>>;
  paramsObject: Record<string, string>;
  resetSearchUrl: () => void;
  setParams: (name: string, value: string) => void;
  urlParams: URLSearchParams;
}

export const useUrlParams = (): UsePrepareUrlParams => {
  const [urlParams, setUrlParams] = useSearchParams();
  const { pathname } = useLocation();

  const paramsObject = Object.fromEntries(urlParams);
  const params = [];

  for (const k in paramsObject) {
    params.push({ [k]: paramsObject[k] });
  }

  const setParams = (name: string, value: string) => {
    urlParams.set(name, value);
    setUrlParams(urlParams);
  };

  const resetSearchUrl = () => {
    setUrlParams([]);
  };

  return { params, paramsObject, setParams, resetSearchUrl, pathname, urlParams };
};
